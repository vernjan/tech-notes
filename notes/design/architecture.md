# Architecture

## Tiers
- logical and physical separation of components
    - **basic tiers**
        - user interface
        - business logic
        - database
    - **more tiers**
        - caches, queues, messaging, load balancers, search servers, ...

### Single-tier
- UI, business logic, database - all on the same machine
- desktop apps, classic PC games
- no network latency
- publisher has no direct control over the app (_patches_ are required)
- reverse-engineering is possible
- risk of inconsistent behavior and look (depends on the user's environment)

### Two-tier (fat client-server)
- **client** - UI and business logic
    - fat (or thick) client
    - browser based games, online games, mobile apps, email client
- **server** - database
    - just storing the state

### Three-tier
- classic web apps
    - UI (HTML, CSS, JS)
    - application server
    - database

### N-tier
- more than 3 basic tiers/components
- single responsibility principle

## Web architecture
- client-server, request-response
- client
    - desktop
    - mobile
    - tablets
- thin client
- client-side rendering
- server-side rendering - faster for browser, but adds up load on backend servers, good for static content

### Client-server communication
- see https://medium.com/geekculture/ajax-polling-vs-long-polling-vs-websockets-vs-server-sent-events-e0d65033c9ba
- **short (Ajax) polling**
    - client polls the server in short intervals, server responds immediately (with data or empty)
- **long polling**
    - client opens a connection to the server and waits for the response
    - once the server responds, client immediately opens a new connection
    - "hanging GET"
- **server-sent events (SSE)**
    - client opens a connection to the server and waits for (many) responses
    - the connection is long-lived and unlike long polling, it's not closed after each response
- **WebSockets**
    - bidirectional communication over TCP
    - HTTP is used just for negotiation (WebSocket handshake)
    - uses the same ports as HTTP (80/443)
- **streaming over HTTP**
    - client opens persistent connection
    - server keeps sending chunks
    - multimedia (video)

## API protocols
- RPC
    - SOAP - XML, verbose, cannot be cached
    - JSON-RPC - over HTTP or WebSockets
    - gRPC
    - Thrift
- REST
    - architectural style
    - specifications - [JSON API](https://jsonapi.org/)
- QL
    - GraphQL

## Shared-nothing architecture
- nodes don't share CPU, disk, database, nothing
- eliminate single point of failure
- easy to add/remove/update nodes

## Peer-to-peer (P2P)
- absence of central server (decentralized), no single point of failure
- nodes have equal rights
- torrents - seeders & leechers
- blockchain

## Reactive
- non-blocking (Akka, Reactor)
- handles lots of open connections

## Proxies
- software or hardware that sits between the client and the server
- caching, filtering, logging, compression, encryption, ...
- **forward proxy** - sits closer to clients, hides their identity
- **reverse proxy** - sits closer to servers, hides their identity