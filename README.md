# Monitoring Stack

## Description

This a local monitoring stack proof of concept that can be spun up locally or in a cluster to improve the visibility of our services. The tool stack is:
* Grafana
* Grafana Loki
* Prometheus
* Web Service
* Alert Manager (_Needs to be added_)

__Note:__ We don't have AlertManager currently as I want to find a solution for this locally.

### Web Service
This is just a 'Hello world' example Nginx web service, this allows us to gather metrics for our monitoring service. You should be able to connect to this service via _http://localhost:8080/_

### Grafana
This is our dashboard which hosts two things mainly for this POC, The Nginx exporter dashboard and the Loki logs. You can connect to Grafana here: _http://localhost:3000/_

To view the dashboard then you need to select _Dashboards_ on the left.
To view the logs, go to _Dropdown_ on the left, then select _logs_

Both of these are automated via [Grafana Provisioning](https://grafana.com/docs/grafana/latest/administration/provisioning/).

### Prometheus
This is used to actually collect the metrics for our web service, we use the [Nginx Exporter](https://github.com/nginx/nginx-prometheus-exporter?tab=readme-ov-file#overview) to query Nginx' Stub status which returns basic metrics.

You can connect to Prometheus via _http://localhost:9090/_

### Grafana Loki
This is used to gather the logs from our webservice (Currently collects all stdout for all containers). We use [promtail](https://grafana.com/docs/loki/latest/send-data/promtail/) which qeuries the local filesystem currently. 

---

## Getting started

This is designed for speed and simplicity, So whilst in the root of the project you can run:

`docker compose up`

That's it, you should now have the monitoring stack up and running.

## Roadmap/Improvements

* Change Promtail to [Alloy](https://grafana.com/docs/loki/latest/setup/migrate/migrate-to-alloy/) as Promtail is now EOL.
* Clean up Log export to only include webservice logs for the POC purpose.
* Add alert manager which a local solution
* Add minio to ship logs to an object store (Mimic S3)
* Add a GitHub actions pipeline to build images and push to a registry.
