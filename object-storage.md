# Blob / Object Storage

Storage systems designed for large, unstructured binary data (images,
videos, backups, logs) — as opposed to structured rows in a database.

## Object storage model
Flat namespace of **buckets** containing **objects**, each identified by
a key (often looks like a file path but isn't a real hierarchical
filesystem). Every object also has metadata (content-type, custom tags).
- **Examples**: Amazon S3, Google Cloud Storage, Azure Blob Storage,
  MinIO (self-hosted, S3-compatible)

```mermaid
graph TD
    Bucket["Bucket: my-app-media"] --> O1["Key: users/42/avatar.jpg"]
    Bucket --> O2["Key: posts/991/photo1.png"]
    Bucket --> O3["Key: videos/raw/clip123.mp4"]
```

## Why not just store files/blobs in the database?
- Databases are optimized for structured, transactional, relatively
  small records — storing multi-MB/GB blobs bloats the DB, slows
  backups, and wastes expensive DB storage/IOPS on data that doesn't
  need transactional guarantees.
- **Standard pattern**: store the actual file in object storage; store
  only a **reference** (URL/key + metadata) in the database.

```mermaid
graph LR
    App[App Server] -->|upload file| S3[(Object Storage)]
    S3 -->|returns URL/key| App
    App -->|store URL + metadata| DB[(Database)]
```

## Key features of object storage systems
- **Durability**: typically "11 nines" (99.999999999%) via erasure
  coding/replication across multiple facilities.
- **Virtually unlimited scale**: no need to pre-provision capacity.
- **Versioning**: keep historical versions of an object.
- **Lifecycle policies**: auto-transition old objects to cheaper "cold"
  storage tiers, or auto-delete after N days.
- **Pre-signed URLs**: generate a temporary, scoped URL that lets a
  client upload/download directly to/from the store without routing
  the bytes through your application servers (huge bandwidth/cost
  savings for large files).

```mermaid
sequenceDiagram
    participant Client
    participant App as App Server
    participant S3 as Object Storage
    Client->>App: Request to upload a file
    App->>S3: Generate pre-signed upload URL
    S3-->>App: pre-signed URL (expires in 5 min)
    App-->>Client: pre-signed URL
    Client->>S3: PUT file directly (bypasses App server)
    S3-->>Client: 200 OK
    Client->>App: Notify upload complete (save metadata)
```

## Chunking large files
For very large uploads (videos, backups), split into chunks uploaded in
parallel and reassembled server-side (multipart upload — supported
natively by S3-compatible APIs). Enables resumable uploads (retry just
the failed chunk, not the whole file).

## Interview tip
Any case study involving user-uploaded media (Instagram, YouTube,
Dropbox) should mention: object storage for the actual bytes, a
CDN in front of it for delivery, pre-signed URLs for direct
client-to-storage upload/download, and only metadata (owner, size,
content-type, storage key) living in your primary database.

## Related
- [CDN](cdn.md)
- [Dropbox case study](../05-case-studies/design-dropbox.md)
- [Instagram case study](../05-case-studies/design-instagram.md)