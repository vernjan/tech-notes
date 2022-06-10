# InfluxDB
- **metrics** (regular) - monitoring
- **events** (irregular) - incoming requests

## Data model
- **database**
    - **measurement** (~ table in a relational DB)
        - **tag** (indexed, for metadata) = tag key + tag value (string)
        - **field** (not-indexed) = field key + field value (floats, booleans, strings, ints)
        - **timestamp**

- **series** - measurement + tag + value
- **point** - measurement + tag + timestamp
