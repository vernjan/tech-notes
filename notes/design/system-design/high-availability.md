# High availability
> ability of the system to stay online despite having failures at the infrastructural level

- reasons for crashes
    - software
    - hardware
    - human error
    - planned downtime
- shared nothing architecture
- at different levels
    - network
    - storage/database
        - locally redundant - withing the same data center
        - zone redundant - across data centers
        - geo redundant - across regions
    - VMs
    - application
- **redundancy** - duplication of critical components (or functions)
- **replication** - sharing information to ensure consistency between redundant resources

## Modes
- **active-active** (load balancing)
    - all nodes are actively running and processing requests
    - there are no standby or passive instances
    - when a single or a few nodes go down, the remaining nodes bear the load of the service
- **active-passive**
    - only one node is actively running (primary) and the backup is on standby (secondary)
        - cold - secondary unit is powered off
        - hot - secondary unit is running (not processing requests)