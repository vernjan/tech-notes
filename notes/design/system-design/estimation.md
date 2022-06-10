# Estimation
- day has 86,400 seconds
- don't forget to multiply the storage requirements by replication factor

## Units

| Name   | Shortcut | 1^x |
|--------|----------|-----|
| piko   | p        | -12 |
| nano   | n        | -9  |
| mikro  | µ        | -6  |
| mili   | m        | -3  |
| -      |          | 0   |
| kilo   | k        | 3   |
| mega   | M        | 6   |
| giga   | G        | 9   |
| tera   | T        | 12  |
| peta   | P        | 15  |

## Powers of Two

| Power | Approx. value  | Unit |
|-------|----------------|------|
| 2^10  | ~1,000         | KiB  |
| 2^20  | ~1 million     | MiB  |
| 2^30  | ~1 billion     | GiB  |
| 2^40  | ~1 trillion    | TiB  |
| 2^50  | ~1 quadrillion | PiB  |

## Latencies
- see https://colin-scott.github.io/personal_website/research/interactive_latency.html

|                               |        |
|-------------------------------|--------|
| L1 cache                      | < 1 ns |
| L2 cache                      | 5 ns   |
| mutex                         | 25 ns  |
| main memory read              | 100 ns |
| SSD read                      | 15 µs  |
| disk seek                     | 2 ms   |
| main memory 1 MB (sequential) | 3 µs   |
| SSD 1 MB (sequential)         | 50 µs  |
| disk 1 MB (sequential)        | 825 µs |
| 2 kB over 1 Gbps network      | 20 µs  |
| data-center roundtrip         | < 1 ms |
| US-EU roundtrip               | 150 ms |

## Availability

| %      | Per day     | Per year  |
|--------|-------------|-----------|
| 99     | 15 minutes  | 3.5 days  |
| 99,9   | 100 seconds | 10 hours  |
| 99,99  | 10 seconds  | 1 hour    |
| 99,999 | 1 second    | 5 minutes |
