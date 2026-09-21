# GitHub Challenge

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

Hey there!

Your challenge is ready.
Follow the instructions provided for this challenge and complete the required tasks in this repository.

Make sure your work is committed and pushed to your repository before submission.

Good luck!


---

&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

--------------------------------------------------------
# TASK1|
In the README, provide a brief description of:
o the service being monitored
o the operational problem being addressed
o the purpose of AIOps in this assessment

This assessment monitors a `payment-service` and its application logs. The collected data includes response time, CPU utilization, memory utilization, log level, timestamps, and service messages.

The problem is to identifying payment-service health issues such as slow responses, database connection timeouts, high CPU usage, and high memory usage.

# Repository Components

- `data/service_data.json`: Sample metrics and service logs.
- `src/anomaly_detector.py`: Detects anomalies 
- `src/event_producer.py`: Publishes detected anomaly events.(produce msgs)
- `src/event_topic.py`: Provides an in-memory event topic.(store messages)
- `src/event_consumer.py`: Consumes published anomaly events.(read msgs)
- `src/aiops_pipeline.py`: Coordinates data loading, anomaly detection, event production, and event consumption.
--------------------------------TASK 1 COMPLETE---------------------------------

# TASK 2

## 1 Metrics fields

- `response_time_ms`: payment request response time.
- `cpu_percent`: CPU utilization percentage.
- `memory_percent`: memory utilization percentage.

The `timestamp` field provides the time context for each metric observation, while `service` identifies the monitored service.

## 2 Log fields

- `log_level`: severity of the log entry, such as `INFO` or `ERROR`.
- `message`: textual description of the event, such as a successful payment or a timeout.

The `service` field also identifies the source of each log entry.

## 3 Use of timestamps

Each record has an timestamp in the format `YYYY-MM-DDTHH:MM:SS`. The observations are recorded at one-minute intervals from `2026-09-20T10:00:00` through `2026-09-20T10:09:00`. Timestamps allow the metrics and log messages to be ordered and correlated, making it possible to see when the service moved from normal operation into an incident and then recovered.

## 4. Normal behaviour

The records at 10:00-10:04 and 10:07-10:09 appear normal. They have:

- response times between 120 and 150 ms;
- CPU utilization between 42% and 50%;
- memory utilization between 51% and 57%;
- `INFO` log levels; and
- the message `Payment request processed successfully`.

These observations show consistent, successful payment processing with moderate resource usage.

## 5. Unusual behaviour

The records at 10:05 and 10:06 appear unusual:

- At 10:05, response time rises to 610 ms and the log reports `Payment service timeout` with level `ERROR`.
- At 10:06, response time rises further to 640 ms, CPU reaches 94%, memory reaches 91%, and the log reports `Database connection timeout` with level `ERROR`.

These two records indicate a short service incident involving high latency, errors, and resource pressure. The return to normal values at 10:07 suggests that the service recovered after the incident.

--------------------------------TASK 2 COMPLETE---------------------------------
# TASK3
The provided AIOps pipeline processed all 10 records from
`data/service_data.json`. The anomaly detector checks response time, CPU
utilization, memory utilization, and error log levels.

## Detection result

- Records processed: 10
- Anomalies detected: 2
- Events consumed: 0

## Detected anomalies

### Observation at 2026-09-20T10:05:00

- Service: `payment-service`
- Response time: `610 ms`
- CPU utilization: `75%`
- Memory utilization: `70%`
- Log level: `ERROR`
- Message: `Payment service timeout`
- Reasons flagged:
  - High response time
  - Error log detected

### Observation at 2026-09-20T10:06:00

- Service: `payment-service`
- Response time: `640 ms`
- CPU utilization: `94%`
- Memory utilization: `91%`
- Log level: `ERROR`
- Message: `Database connection timeout`
- Reasons flagged:
  - High response time
  - High CPU utilization
  - High memory utilization
  - Error log detected

## Normal and anomalous observations

The records from 10:00 to 10:04 and from 10:07 to 10:09 were treated as
normal. They contain successful payment messages, `INFO` log levels, response
times between 120 and 150 ms, CPU utilization between 42% and 50%, and memory
utilization between 51% and 57%.

The records at 10:05 and 10:06 were correctly identified as anomalous. They
contain high response times and `ERROR` logs. The 10:06 observation also shows
high CPU and memory utilization.

# No expected anomaly appears to have been missed, and no normal observation
# appears to have been incorrectly flagged in this dataset.

## Detection limitation

The detector uses fixed thresholds and simple rules. It does not learn the
normal behavior of the service or detect gradual changes over time. A possible
improvement would be to calculate dynamic thresholds from historical data and
correlate related metrics with log events.

## Pipeline issue

Although two anomalies were detected, the final output shows zero events
consumed. The producer publishes events to the `service-events` topic, while
the consumer reads from the separate `anomaly-events` topic. Because the
topics are different, the detected events are not displayed in the consumed
events report. This is a configuration issue in the provided pipeline.
-----------------------------------task 3 completed------------------------------------------
