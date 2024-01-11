# Guice

## Mental model

https://github.com/google/guice/wiki/MentalModel

- Guice is a map of **keys** to **providers**
    - **key**: type + optional annotation
    - **provider**: function that returns an instance of the type (`T get()`)