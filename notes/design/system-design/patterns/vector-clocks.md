# Vector Clocks
> algorithm that generates partial ordering of events and detects causality violations in a distributed system

- build on Lamport clocks, but we keep track of events for each node (for example `<2,2,0>` means 2 events on node A, 2 events on node B and so)
    - incrementing and merging is similar to Lamport clocks, it's just done for each vector element individually
- every object (and every object version, or just think any event) has associated a vector clock timestamp
- `V(a) < V(b) <=> a -> b` - unlike Lamport, this holds in both directions
- sounds a bit complicated, but it's actually quite straightforward - comparing the vectors tell us if `a` happened before `b`
    - all vector elements must be smaller or equal (if all are equal, then it's the same event)
- conflict detection
    - some scenarios can be auto resolved, some scenarios require client interaction (such as _merge_ or a custom logic)
- Different replicas of an object can end up with different versions of the data