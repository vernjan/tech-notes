# Compatibility

## Sources
- [Backward vs. Forward Compatibility](https://stevenheidel.medium.com/backward-vs-forward-compatibility-9c03c3db15c9)

## Backward
- **new consumer can read from existing producers (can process existing data)**
    - Java 17 can run Java 11 bytecode
    - new version of app can read data from database written from the previous version
    - new version of web app can process HTTP responses from a server
        - so for example new version must not expect a new mandatory field (without a default value)

## Forward
- **new producer doesn't break existing consumers**
    - new version of server API can't break existing clients
    - new version of a client posting data to the server can't break the server

## Consumer vs. producer
- **client - server**
    - client is consumer when getting data from server (server is producer)
    - client is producer when posting data to the server (server is consumer)
- **database**
    - producer is the app writing the data, consumer is the app reading the data


