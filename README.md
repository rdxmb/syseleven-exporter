# SysEleven Exporter

> This project is a fork of the original [syseleven-exporter](https://github.com/Staffbase/syseleven-exporter) created by [Staffbase](https://github.com/Staffbase/).

Export your quota and current usage from the SysEleven API as Prometheus metrics. The exporter uses the `https://api.cloud.syseleven.net:5001` API endpoint to get the quota and usage statistics for all SysEleven resources.

The SysEleven Exporter can be deployed using the [vfm/syseleven-exporter-chart](https://github.com/vfm/syseleven-exporter-chart/) Helm chart.

## Usage

Clone the repository and build the binary:

```sh
git clone git@github.com:syseleven/syseleven-exporter.git
make build
```

Set the environment variables for authentication against the SysEleven API.
There are two authentication options available:

- Username and password

  ```sh
  export OS_USERNAME=
  export OS_PASSWORD=
  # OS_PROJECT_ID could be a comma separated list of project IDs
  export OS_PROJECT_ID=
  ```

- Application credentials (do **not** set `OS_PROJECT_ID`)

  ```sh
  export OS_APPLICATION_CREDENTIAL_ID=
  export OS_APPLICATION_CREDENTIAL_SECRET=
  ```

  *Note that when using application credentials you cannot specify `OS_PROJECT_ID`.*
  *Else the authentication won't work. Also this means that you can only scrape metrics for one project.*
  *This will be the project the application credentials are created in and scoped to.*

- Optional: Configure API endpoints for non standard (not `https://keystone.cloud.syseleven.net:5000/v3`
and `https://api.cloud.syseleven.net:5001`)

  ```sh
  export OS_AUTH_URL="https://api.example.syseleven.de:5000"
  export SYSELEVEN_QUOTA_API_ENDPOINT="https://api.example.syseleven.de:5001"
  ```

Then run the exporter:

```sh
./bin/syselevenexporter
```

A Docker image is available at `syseleven/syseleven-exporter:<TAG>` and can be retrieved via:

```sh
docker pull syseleven/syseleven-exporter:<TAG>
```

## Metrics

| Metric | Description |
| ------ | ----------- |
| syseleven_compute_cores_total | Quota for number of compute cores per `region` and `project` |
| syseleven_compute_cores_used | Number of used compute cores per `region` and `project` |
| syseleven_compute_instances_total | Quota for number of compute instances per `region` and `project` |
| syseleven_compute_instances_used | Number of used compute instances per `region` and `project` |
| syseleven_compute_flavors_used | Number of used compute flavors per `type` and `region` and `project` |
| syseleven_compute_ram_total_megabytes | Quota for ram per `region` and `project` in megabytes |
| syseleven_compute_ram_used_megabytes | Used ram per `region` and `project` in megabytes |
| syseleven_dns_zones_total | Quota for number of DNS zones per `region` and `project` |
| syseleven_dns_zones_used | Number of used DNS zones per `region` and `project` |
| syseleven_network_floating_ips_total | Quota for number of floating IPs per `region` and `project` |
| syseleven_network_floating_ips_used | Number of used floating IPs per `region` and `project` |
| syseleven_network_loadbalancers_total | Quota for number of load balancers per `region` and `project` |
| syseleven_network_loadbalancers_used | Number of used load balancers per `region` and `project` |
| syseleven_s3_space_total_bytes | Quota for S3 space per `region` and `project` in bytes |
| syseleven_s3_space_used_bytes | Used S3 space per `region` and `project` in bytes |
| syseleven_volume_space_total_gigabytes | Quota for volume space per `region` and `project` in gigabytes |
| syseleven_volume_space_used_gigabytes | Number of used volume space per `region` and `project` in gigabytes |
| syseleven_volume_volumes_total | Quota for number of volumes per `region` and `project` |
| syseleven_volume_volumes_used | Number of used volumes per `region` and `project` |

## Credits

- [Staffbase](https://github.com/Staffbase/) - Original Author
- [vfm](https://github.com/vfm) - Original Author of the Helm chart
