# CQRS (Command and Query Responsibility Segregation)
- standard approach is having one conceptual model and use CRUD
- CQRS brings 2 models -  one for updating information (_command model_) and one for reading information (_query model_)
- separates read and writes - allows scaling writes and reads separately
- database can be shared (we have 2 different object/in-memory models) or even database can be different
- usually combined with event sourcing (events are aggregated and somehow processed before being read)

## Sources
- [CQRS](https://martinfowler.com/bliki/CQRS.html) (Martin Fowler)