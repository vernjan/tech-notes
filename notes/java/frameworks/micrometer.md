# Micrometer

- universal facade (SDK) for application observability (metrics and tracing, not logs)
- vendor-neutral
- Java only
- new global standard for all languages is **OpenTelemetry** (OTel)
    - Micrometer can be used as a bridge to OTel
    - OTel also supports logs, i.e. all 3 pillars of observability (metrics, logs, traces)
- Micrometer defines concepts (metric types - counter, timer, gauge; tags) and offers many "exporters" to popular monitoring tools
    - Prometheus, InfluxDB, Graphite, Ganglia, StatsD, Datadog, ..
    - provides concept implementation - code instrumentation, AOP
- Micrometer is modeled after Prometheus
  - multi-dimensional - tags
    
