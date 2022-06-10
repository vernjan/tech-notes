# Leader - Followers
- doesn't necessarily mean there is just one leader - a leader can be, for example, per partition
- leader accepts writes and replicates data to followers
- followers may or may not be used for reads
- followers are ready to replace leader in case of crash (leader election)