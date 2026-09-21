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

- `data/service_data.json`: Sample operational metrics and service logs.
- `src/anomaly_detector.py`: Detects anomalies using response-time, CPU, memory, and log-level thresholds.
- `src/event_producer.py`: Publishes detected anomaly events.
- `src/event_topic.py`: Provides an in-memory event topic.
- `src/event_consumer.py`: Consumes published anomaly events.
- `src/aiops_pipeline.py`: Coordinates data loading, anomaly detection, event production, and event consumption.
--------------------------------TASK 1 COMPLETE---------------------------------