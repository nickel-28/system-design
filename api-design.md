# API Design: REST vs GraphQL vs gRPC

## REST (Representational State Transfer)
Resource-oriented, uses HTTP verbs and status codes.
```
GET    /users/123          → fetch user 123
POST   /users               → create a user
PUT    /users/123           → replace user 123
PATCH  /users/123           → partially update user 123
DELETE /users/123           → delete user 123
```
- **Pros**: simple, cacheable (via HTTP semantics), huge tooling/ecosystem,
  stateless, human-readable.
- **Cons**: over-fetching (returns fixed shape even if client needs less)
  or under-fetching (client needs multiple round-trips for related
  resources — the classic N+1 problem on the client side).

## GraphQL
Client specifies exactly the fields/shape it needs in a single query.
```graphql
query {
  user(id: "123") {
    name
    posts(limit: 5) { title, likes }
  }
}
```
- **Pros**: no over/under-fetching, single round trip for nested/related
  data, strongly typed schema, great for mobile clients (bandwidth
  matters) and rapidly evolving frontends.
- **Cons**: harder to cache at the HTTP layer (mostly POST requests to a
  single endpoint), risk of expensive/nested queries hurting the server
  (needs query complexity limits/depth limiting), more server-side
  complexity (resolvers, N+1 query problem needs `DataLoader`-style
  batching).

## gRPC
Binary protocol (Protocol Buffers) over HTTP/2, contract-first (`.proto`
files generate client/server code).
```protobuf
service UserService {
  rpc GetUser (UserRequest) returns (UserResponse);
}
```
- **Pros**: very fast (binary serialization, HTTP/2 multiplexing),
  strongly typed contracts, built-in streaming (client/server/bidi),
  great for internal service-to-service communication.
- **Cons**: not human-readable, browser support is limited (needs
  grpc-web/proxy), steeper learning curve, less ideal for public APIs
  consumed by third parties.

## Decision table
| Situation | Best fit |
|---|---|
| Public API for third-party developers | REST (familiar, cacheable, easy to document) |
| Mobile app with varied/nested data needs | GraphQL |
| Internal microservice-to-microservice calls (high volume, low latency) | gRPC |
| Simple CRUD app | REST |
| Need real-time bidirectional streaming between services | gRPC (streaming) or WebSockets |

## Good API design practices (any style)
- **Versioning**: `/v1/users` or header-based versioning — never break
  existing clients silently.
- **Pagination**: cursor-based (`?after=<opaque_cursor>`) scales better
  than offset-based (`?page=5`) for large/changing datasets (offset
  pagination re-scans skipped rows and shifts under concurrent writes).
- **Idempotency**: `PUT`/`DELETE` should be idempotent by design; for
  `POST` (e.g., payments), accept an `Idempotency-Key` header so retries
  don't double-charge.
- **Rate limiting**: return `429 Too Many Requests` with a `Retry-After`
  header — see [rate-limiting.md](rate-limiting.md).
- **Consistent error format**: a standard `{ "error": { "code":
  "...", "message": "..." } }` shape across all endpoints.
- **HATEOAS** (REST maturity level 3): responses include links to
  related actions — rarely fully implemented in practice, but good to
  know as a concept.

## Interview tip
When a case study says "design the API for X," write out 4–6 concrete
endpoints with method, path, request/response shape — this is a fast,
concrete way to demonstrate you've internalized the data model.

## Related
- [Rate limiting](rate-limiting.md)
- [Rate Limiter case study](../05-case-studies/design-rate-limiter.md)