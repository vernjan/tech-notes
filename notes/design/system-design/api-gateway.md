# API Gateway
- an entry point for external clients
- has information about (internal) endpoints
- capable of
    - authentication
    - caching
    - logging
    - rate limiting
    - load balancing
    - managing access quotas
    - API health monitoring
    - API versioning
    - A/B testing
    - analytics
    - response aggregation/transformation from multiple microservices
- L7 layer

## Sources
- [14 Open Source and Managed API Gateway for Modern Applications](https://geekflare.com/api-gateway/)
- [How To Configure API Gateway in Microservices Architecture](https://marutitech.com/api-gateway-in-microservices-architecture/)

## API gateway vs. service mesh
- some responsibilities overlap (load balancing, routing, monitoring, rate limiting) but
    - **API gateway** is for client -> service communication
    - **service mesh** is for service -> service communication

## Examples
- [Netflix Zuul](https://github.com/Netflix/zuul)
    - dynamic routing, monitoring, resiliency, security, and more
- Kong Gateway
    - most popular open-source cloud-native API gateway
    - nginx + Lua
- Apache APISIX
    - nginx + etcd
- Apigee
- Amazon API Gateway