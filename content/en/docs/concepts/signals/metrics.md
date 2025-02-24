---
title: Metrics
weight: 2
---

A **metric** is a measurement about a service, captured at runtime. Logically,
the moment of capturing one of these measurements is known as a _metric event_
which consists not only of the measurement itself, but the time that it was
captured and associated metadata.

Application and request metrics are important indicators of availability and
performance. Custom metrics can provide insights into how availability
indicators impact user experience or the business. Collected data can be used to
alert of an outage or trigger scheduling decisions to scale up a deployment
automatically upon high demand.

OpenTelemetry defines six _metric instruments_ today which can be created
through the OpenTelemetry API:

- **Counter**: A value that accumulates over time -- you can think of this like
  an odometer on a car; it only ever goes up.
- **Asynchronous Counter**: Same as the **Counter**, but is collected once for
  each export. Could be used if you don't have access to the continous
  increments, but only to the aggregated value.
- **UpDownCounter**: A value that accumulates over time, but can also go down
  again. An example could be a queue length, it will increase and decrease with
  the number of work items in the queue.
- **Asynchronous UpDownCounter**: Same as the **UpDownCounter**, but is
  collected once for each export. Could be used if you don't have access to the
  continous changes, but only to the aggregated value (e.g., current queue
  size).
- **(Asynchronous) Gauge**: Measures a current value at the time it is read. An
  example would be the fuel gauge in a vehicle. Gauges are _always_
  asynchronous.
- **Histogram**: A histogram is a client-side aggregation of values, e.g.,
  request latencies. A histogram is likely a good choice if you have a lot of
  values, and are not interested in every individual value, but a statistic
  about these values (e.g., How many requests take fewer than 1s?)

In addition to the metric instruments, the concept of _aggregations_ is an
important one to understand. An aggregation is a technique whereby a large
number of measurements are combined into either exact or estimated statistics
about metric events that took place during a time window. The OTLP protocol
transports such aggreagated metrics. The OpenTelemetry API provides a default
aggregation for each instrument which can be overridden using the Views API. The
OpenTelemetry project aims to provide default aggregations that are supported by
visualizers and telemetry backends.

Unlike request tracing, which is intended to capture request lifecycles and
provide context to the individual pieces of a request, metrics are intended to
provide statistical information in aggregate. Some examples of use cases for
metrics include:

- Reporting the total number of bytes read by a service, per protocol type.
- Reporting the total number of bytes read and the bytes per request.
- Reporting the duration of a system call.
- Reporting request sizes in order to determine a trend.
- Reporting CPU or memory usage of a process.
- Reporting average balance values from an account.
- Reporting current active requests being handled.

> For more information, see the [metrics specification][].

[metrics specification]: /docs/reference/specification/overview/#metric-signal
