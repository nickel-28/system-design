# System Design Interview Preparation

A structured, self-contained guide for system design interviews — covering
core fundamentals, building blocks, architecture patterns, a repeatable
interview framework, 15 fully worked case studies (the classic questions
asked at FAANG-tier interviews), and low-level/OOP design.

Every topic is written as standalone notes with diagrams (rendered with
Mermaid, so they display natively on GitHub) and trade-off tables — the
same way you should reason out loud in an interview.

## How to use this repo
- New to system design? Read `01-fundamentals` → `02-building-blocks` →
  `04-interview-approach` in order, then start doing case studies.
- Cramming before an interview? Skim `04-interview-approach/framework.md`,
  then work through 4–5 case studies in `05-case-studies` out loud, on a
  whiteboard, without looking at the answer first.
- Asked about OOP/LLD instead of HLD? Go straight to `06-low-level-design`.

---

## 📚 Table of Contents

### 1. Fundamentals (`01-fundamentals/`)
| Topic | File |
|---|---|
| Scalability (vertical vs horizontal) | [scalability.md](01-fundamentals/scalability.md) |
| Availability & Reliability | [availability-reliability.md](01-fundamentals/availability-reliability.md) |
| Consistency models | [consistency-models.md](01-fundamentals/consistency-models.md) |
| CAP & PACELC theorem | [cap-theorem.md](01-fundamentals/cap-theorem.md) |
| Latency, throughput & back-of-envelope math | [latency-throughput.md](01-fundamentals/latency-throughput.md) |

### 2. Building Blocks (`02-building-blocks/`)
| Topic | File |
|---|---|
| Load balancing | [load-balancing.md](02-building-blocks/load-balancing.md) |
| Caching | [caching.md](02-building-blocks/caching.md) |
| SQL vs NoSQL | [databases-sql-vs-nosql.md](02-building-blocks/databases-sql-vs-nosql.md) |
| Indexing & sharding | [database-indexing-sharding.md](02-building-blocks/database-indexing-sharding.md) |
| Replication | [replication.md](02-building-blocks/replication.md) |
| Message queues & streaming | [message-queues.md](02-building-blocks/message-queues.md) |
| API design (REST/GraphQL/gRPC) | [api-design.md](02-building-blocks/api-design.md) |
| CDN | [cdn.md](02-building-blocks/cdn.md) |
| Proxy & reverse proxy | [proxy-reverse-proxy.md](02-building-blocks/proxy-reverse-proxy.md) |
| Rate limiting | [rate-limiting.md](02-building-blocks/rate-limiting.md) |
| Consistent hashing | [consistent-hashing.md](02-building-blocks/consistent-hashing.md) |
| Microservices vs monolith | [microservices-vs-monolith.md](02-building-blocks/microservices-vs-monolith.md) |
| WebSockets, polling & SSE | [realtime-communication.md](02-building-blocks/realtime-communication.md) |
| Blob/object storage | [object-storage.md](02-building-blocks/object-storage.md) |

### 3. Architecture Patterns (`03-architecture-patterns/`)
| Topic | File |
|---|---|
| Event-driven architecture | [event-driven-architecture.md](03-architecture-patterns/event-driven-architecture.md) |
| CQRS & Event Sourcing | [cqrs-event-sourcing.md](03-architecture-patterns/cqrs-event-sourcing.md) |
| Saga pattern (distributed transactions) | [saga-pattern.md](03-architecture-patterns/saga-pattern.md) |

### 4. Interview Approach (`04-interview-approach/`)
| Topic | File |
|---|---|
| A repeatable framework for any question | [framework.md](04-interview-approach/framework.md) |
| Back-of-envelope estimation cheatsheet | [estimation-cheatsheet.md](04-interview-approach/estimation-cheatsheet.md) |

### 5. Case Studies — Standard Interview Problems (`05-case-studies/`)
| # | Problem | File |
|---|---|---|
| 1 | URL Shortener (TinyURL) | [design-url-shortener.md](05-case-studies/design-url-shortener.md) |
| 2 | Pastebin | [design-pastebin.md](05-case-studies/design-pastebin.md) |
| 3 | Rate Limiter | [design-rate-limiter.md](05-case-studies/design-rate-limiter.md) |
| 4 | Distributed Key-Value Store | [design-key-value-store.md](05-case-studies/design-key-value-store.md) |
| 5 | Twitter / News Feed | [design-twitter.md](05-case-studies/design-twitter.md) |
| 6 | Instagram | [design-instagram.md](05-case-studies/design-instagram.md) |
| 7 | WhatsApp / Chat System | [design-chat-system.md](05-case-studies/design-chat-system.md) |
| 8 | Uber / Ride-Hailing | [design-uber.md](05-case-studies/design-uber.md) |
| 9 | YouTube / Netflix (Video Streaming) | [design-video-streaming.md](05-case-studies/design-video-streaming.md) |
| 10 | Web Crawler | [design-web-crawler.md](05-case-studies/design-web-crawler.md) |
| 11 | Typeahead / Autocomplete Search | [design-typeahead.md](05-case-studies/design-typeahead.md) |
| 12 | Notification System | [design-notification-system.md](05-case-studies/design-notification-system.md) |
| 13 | Dropbox / Google Drive | [design-dropbox.md](05-case-studies/design-dropbox.md) |
| 14 | Ticketmaster (Event Booking) | [design-ticketmaster.md](05-case-studies/design-ticketmaster.md) |
| 15 | Distributed Cache | [design-distributed-cache.md](05-case-studies/design-distributed-cache.md) |

### 6. Low-Level Design / OOP (`06-low-level-design/`)
| Topic | File |
|---|---|
| OOP principles & SOLID | [oop-and-solid.md](06-low-level-design/oop-and-solid.md) |
| Common design patterns | [design-patterns.md](06-low-level-design/design-patterns.md) |
| LLD: Parking Lot | [lld-parking-lot.md](06-low-level-design/lld-parking-lot.md) |
| LLD: Elevator System | [lld-elevator-system.md](06-low-level-design/lld-elevator-system.md) |

### 7. Resources (`07-resources/`)
| Topic | File |
|---|---|
| Books, papers, courses, links | [resources.md](07-resources/resources.md) |

---

## 🗺️ Suggested 4-week study plan

| Week | Focus |
|---|---|
| 1 | Fundamentals + Building Blocks (read + take notes in your own words) |
| 2 | Architecture patterns + Interview framework + Estimation drills |
| 3 | Case studies 1–8 (do each one timed, 35–45 min, before reading the answer) |
| 4 | Case studies 9–15 + Low-level design + 2 full mock interviews |

## 🤝 Contributing
This repo is meant to be a living document. Feel free to fork it, add your
own case studies, correct mistakes, or add diagrams for topics that need
them.

## 📄 License
MIT — use freely for your own prep or to help others prepare.