# Databases

- [Relational databases](relational-databases.md)
- [Prometheus](prometheus.md)
- [NoSQL](nosql.md)

## Character sets and collations

- https://dev.mysql.com/doc/refman/8.4/en/charset-general.html
- **character set**
    - a set of symbols and encodings (`latin1`, `utf8mb4`, ...)
    - affects how data is stored and handled, for example what's the length of 😀? Functions like `LENGTH()` or `SUBSTRING()`
- **collation**
    - rules for comparing and sorting characters
    - e.g. sorting of Czech `ch`, or comparing German `ß == ss`
    - `lower/upper` conversions
    - binary collation - compares strings based on their binary values (encodings)
- it's also important to set the correct character set for the database connection
    - `mysql --default-character-set=utf8mb4 my_db` 