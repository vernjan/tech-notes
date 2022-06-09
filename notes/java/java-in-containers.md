# Java in Containers
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
- [JVM in a Container](https://www.merikan.com/2019/04/jvm-in-a-container/) (Merikan blog)
- [Java 17: What’s new in OpenJDK's container awareness](https://developers.redhat.com/articles/2022/04/19/java-17-whats-new-openjdks-container-awareness?utm_source=pocket_mylist) (RedHat)
