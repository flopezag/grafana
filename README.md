# FIWARE Grafana Instances

This project deploy automatically Grafana instances, configured to show the historical information
of the Monitoring data. The project is configured to automatically deploy several instances
depending of the environment variable **_SERVICE_**. The expected values are:

| **_SERVICE_ enviornment value**  | **Description**                                                        |
|----------------|---------------------------------------------------------------------|
| fiware-sla     | Grafana configuration for the FIWARE SLA monitoring tool dashboard. |
| fiware-metrics | Grafana configuration for the FIWARE GEs metrics dashboard.         |
| orion-cef      | Grafana configuration for the Orion in CEF dashboard.               |

These values has to be defined inside the .env file

## Requirements

In order to excute this project to need to have the following components:

* docker engine (Docker version 19.03.1, build 74b1e89)
* docker compose (docker-compose version 1.24.1, build 4667896b)

## Preconfiguration

This project is a docker-compose project that deploy the last version of grafana docker image
with a configuration for datasources and dashboards specific for each case.

Before launching the docker-compose it is needed a preconfiguration of the sensible information, 
please configure the proper information in the following files:

| **File**                                                     | **Field**                  | **Value**                                                |
|--------------------------------------------------------------|----------------------------|----------------------------------------------------------|
| ./configs/$(SERVICE)/provisioning/datasources/datasource.yml | user                       | User account of the InfluxDB service.                    |
|                                                              | password                   | Password of the corresponding user.                      |
|                                                              | url                        | InfluxDB instance url.                                   |
|                                                              | database                   | Name of the InfluxDB instance with the monitoring data.  |
| ./configs/config.grafana                                     | GF_SECURITY_ADMIN_PASSWORD | Default admin password of the deployed Grafana instance. |

## Run

In order to execute the composer just run:

```console
docker-compose up -d
```

To stop the Gradana compose instance just run:

```console
docker-compose down
```

Keep in mind that the docker-compose was deployed with a local volume _grafana_data_, therefore keep in mind that this 
directory will stay there after the down operation, at least that you manually delete it.

## License

These scripts are licensed under Apache License 2.0.


