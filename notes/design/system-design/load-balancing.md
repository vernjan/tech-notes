# Load Balancing
- capabilities
    - endpoint discover
    - health check
    - load balancing
- HA - load balancer must not be a single point of failure - redundancy (active-passive)

## Sources
- [Understand Cloud Load Balancer Like a Senior Engineer](https://medium.com/google-cloud/understand-cloud-load-balancer-like-a-senior-engineer-d4f55f3111fc) (Google cloud)
- [System Design — Load Balancing](https://medium.com/must-know-computer-science/system-design-load-balancing-1c2e7675fc27) (Medium blog)

## L4 vs. L7

### L4
- acts upon L4 layer (IP + TCP/UDP)
- **Direct Server Return** (DSR)
    - LB changes MAC address
    - connection is directly between client and server
        - response goes directly to the client (avoids LB)
- **NAT mode**
    - LB changes destination IP address
    - both requests and responses pass through LB

### L7
- acts upon L7 layer (application layer - access to HTTP headers, path)
- `X-Forwarded-For` header and similar
- 2 TCP connections - client-LB and LB-server
- TLS termination - need access to request data

## Types
- **DNS based**
    - DNS authoritative server can return different IP addresses to clients
    - returns list of IP addresses - in case of failure, client can use a different address
        - unlike classic load balancers, authoritative server has no knowledge of the targeted system health
    - round-robin, geo
- **hardware**
    - highly performant physical hardware
    - costly purchase and maintenance
    - Big-5, Netscaler
- **software**
    - developers prefer software LB - easier deployment and configuration
    - more options compared to DNS load balancing
        - access to metrics from downstream servers
        - access to HTTP headers, path (for L7)
    - HAProxy, nginx

## Algorithms
- **round-robin** - homogenous downstream servers, not persistent connections
- **weighted round-robin** - heterogeneous downstream servers
- **least connections**
    - handy for long-opened (persistent) connections (for example gaming applications)
- **random**
- **hash**
    - IP based hash - client is routed to the same server
        - server can hold user data