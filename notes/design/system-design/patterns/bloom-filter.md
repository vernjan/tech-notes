# Bloom Filter
- see https://www.educative.io/edpresso/what-is-a-bloom-filter
- probabilistic data structure
- highly space efficient (does not store the actual items, just a few bits from hash)
- answers the question "Does it contain the element?"
    - **false positive is possible** - if bloom filter tells it contains, it's not necessarily true
    - **false negative is impossible** - if bloom filter tells it doesn't contain, then it never does
    - **tl;dr** "might be in a set, or definitely is not"
