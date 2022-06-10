# Gossip Protocol
- decentralized nodes
- peer-to-peer communication mechanism
    - to keep track which nodes are alive
    - or exchanging any other data (key ranges)
- everyone talking to each other would be `N^2` messages
- How it works?
    - forward message to 3 random nodes, after a few rounds, there is high probability that all nodes were reached
- Dynamo, Cassandra