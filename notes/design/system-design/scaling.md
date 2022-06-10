# Scaling

## Scaling tips
- stateless web tier (no sticky sessions)
  - - stateless web tier - no user data (sessions) on web servers
  - to enable horizontal scaling and failover
  - TODO avoid sticky sessions
- build redundancy at every level (avoid single point of failure)
- caching, CDN
- sharding
- monitoring

### Vertical vs. horizontal scaling
- **vertical scaling** (scaling up)
  - "easy" but has hard limits and offers no redundancy
- **horizontal scaling** (scaling out)
  - brings a risk of data inconsistency

## Latency
- network and application