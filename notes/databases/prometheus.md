# Prometheus

- time-series database
- monitoring & alerting

## Metrics

- **name + labels**: value, timestamp (ms)
    - name + labels form a metric keys (individual time series)
    - value is a float
- 4 types of metrics
    - **counters** - ever-increasing values (e.g. errors counter)
        - resets only when the process/app restarts
    - **gauges** - fluctuating values (e.g. CPU usage)
        - long scrape intervals can miss spikes
    - **histograms** - distribution of values into predefined buckets (e.g. request duration or size)
        - list of buckets (counters) + sum + count
        - by default, histogram buckets are preconfigured for time duration (5ms, 10ms, 25ms, 50ms, 100ms, 250ms, 500ms, 1s, ...)
          but can be changed to e.g. size in bytes
    - **summaries** - distribution of values into quantiles (percentiles)
        - list of quantiles (counters) + sum + count
            - 0.0 quantile is the min
            - 1.0 quantile is the max
        - quantiles are configurable and optional, if omitted ten sum & count only
        - by default, calculated based on the 5-minute moving window
        - quantiles cannot be aggregated
- each metrics has a **name** and a set of **labels** (key-value pairs)

In general, you should prefer histograms to summaries. The Prometheus query language has a function `histogram_quantile()` for calculating
quantiles from histograms. The advantage of query-time quantile calculation is that you can aggregate histograms before calculating the
quantile. See https://prometheus.io/docs/practices/histograms/#quantiles

### Example 1: Simple gauge

```
# HELP application_ready_time_seconds Time taken for the application to be ready to service requests
# TYPE application_ready_time_seconds gauge
application_ready_time_seconds{main_application_class="com.purestorage.integrations.vmware.pureplugin.server.PurePluginServerApplication"} 11.789
```

### Example 2: Multi-gauge

A single metric can have multiple instances with different labels.

```
# HELP jvm_memory_committed_bytes The amount of memory in bytes that is committed for the Java virtual machine to use
# TYPE jvm_memory_committed_bytes gauge
jvm_memory_committed_bytes{area="heap",id="G1 Eden Space"} 1.13246208E8
jvm_memory_committed_bytes{area="heap",id="G1 Old Gen"} 1.63577856E8
jvm_memory_committed_bytes{area="heap",id="G1 Survivor Space"} 4194304.0
jvm_memory_committed_bytes{area="nonheap",id="CodeCache"} 1.769472E7
jvm_memory_committed_bytes{area="nonheap",id="Compressed Class Space"} 1.3303808E7
jvm_memory_committed_bytes{area="nonheap",id="Metaspace"} 8.454144E7
```

### Example 3: Static gauge

A metric can have a static value and use labels to export additional info.

```
# HELP jvm_info JVM version info
# TYPE jvm_info gauge
jvm_info{runtime="OpenJDK Runtime Environment",vendor="Eclipse Adoptium",version="17.0.8.1+1"} 1
```

### Example 4: Histogram

`_bucket` - number of observations in each bucket (`le` stands for _less than or equal to_)

```
# HELP http_request_duration_seconds Histogram of HTTP request durations in seconds
# TYPE http_request_duration_seconds histogram
http_request_duration_seconds_bucket{le="0.05"} 11
http_request_duration_seconds_bucket{le="0.1"} 11
http_request_duration_seconds_bucket{le="0.25"} 35
http_request_duration_seconds_bucket{le="0.5"} 77
http_request_duration_seconds_bucket{le="1"} 77
http_request_duration_seconds_bucket{le="2.5"} 77
http_request_duration_seconds_bucket{le="5"} 77
http_request_duration_seconds_bucket{le="10"} 77
http_request_duration_seconds_bucket{le="+Inf"} 77
http_request_duration_seconds_sum 19.730312268000002
http_request_duration_seconds_count 77
```