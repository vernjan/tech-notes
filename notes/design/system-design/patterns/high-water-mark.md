# High-water Mark
- to prevent inconsistencies between a leader and followers
- high-water mark points to the latest data (message) already replicated to followers
- leader doesn't expose data above high-water mark
    - simply because in case it fails, those data could be lost forever causing non-repeatable reads