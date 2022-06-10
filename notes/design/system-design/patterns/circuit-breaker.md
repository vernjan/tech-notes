# Circuit Breaker
- wraps a call to a remote system (for example outbound HTTP call)
- if the call keeps failing (timeouts), the circuit breaker triggers and stops sending new calls, instead it just returns errors
- after some time, the circuit breaker checks if the remote system is operational again, if so, it passes through new calls
- the goal is to prevent cascading failures

## Sources
- [CircuitBreaker](https://martinfowler.com/bliki/CircuitBreaker.html) (Martin Fowler)