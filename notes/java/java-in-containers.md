# Java in Docker
- newer Java - better support
    - understands `docker --cpu 2`
- JVM ergonomics - auto-tuning based on the runtime environment (gc, heap size, compiler)
- **class data sharing** (CDS)
    - re-use class loading outputs - faster startups
    - enabled by default
- `jlink` to create a custom (minimal) JRE
    - `jdeps` to determine required modules
    - use multi-stage builds

## Sources
- [](https://www.merikan.com/2019/04/jvm-in-a-container/)

