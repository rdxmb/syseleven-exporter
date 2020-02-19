# SysEleven Exporter

Export your quota and current usage from the SysEleven API as Prometheus metrics. The exporter uses the `https://api.cloud.syseleven.net:5001` API endpoint to get the quota and usage statistics for all SysEleven resources.

## Usage

Clone the repository and build the binary:

```sh
git clone git@github.com:Staffbase/syseleven-exporter.git
make build
```

Set the environment variables for authentication against the SysEleven API:

```sh
export OS_USERNAME=
export OS_PASSWORD=
export OS_PROJECT_ID=
```

Then run the exporter:

```sh
./bin/syselevenexporter
```

A Docker image is available at `registry.staffbase.com/public/syseleven-exporter:<TAG>` and can be retrieved via:

```sh
docker pull registry.staffbase.com/public/syseleven-exporter:<TAG>
```

## Metrics

| Metric | Description |
| ------ | ----------- |
| syseleven_compute_cores_total | Quota for number of compute cores per `region` |
| syseleven_compute_cores_used | Number of used compute cores per `region` |
| syseleven_compute_instances_total | Quota for number of compute instances per `region` |
| syseleven_compute_instances_used | Number of used compute instances per `region` |
| syseleven_compute_flavors_used | Number of used compute flavors per `type` and `region` |
| syseleven_compute_ram_total_megabytes | Quota for ram per `region` in megabytes |
| syseleven_compute_ram_used_megabytes | Used ram per `region` in megabytes |
| syseleven_dns_zones_total | Quota for number of DNS zones per `region` |
| syseleven_dns_zones_used | Number of used DNS zones per `region` |
| syseleven_network_floating_ips_total | Quota for number of floating IPs per `region` |
| syseleven_network_floating_ips_used | Number of used floating IPs per `region` |
| syseleven_network_loadbalancers_total | Quota for number of load balancers per `region` |
| syseleven_network_loadbalancers_used | Number of used load balancers per `region` |
| syseleven_s3_space_total_bytes | Quota for S3 space per `region` in bytes |
| syseleven_s3_space_used_bytes | Used S3 space per `region` in bytes |
| syseleven_volume_space_total_gigabytes | Quota for volume space per `region` in gigabytes |
| syseleven_volume_space_used_gigabytes | Number of used volume space per `region` in gigabytes |
| syseleven_volume_volumes_total | Quota for number of volumes per `region` |
| syseleven_volume_volumes_used | Number of used volumes per `region` |
