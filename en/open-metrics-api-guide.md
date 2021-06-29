## Compute > System Monitoring > API Guide

### Basic information
```http
API Endpoint: https://kr1-api-sysmon.cloud.toast.com
```

## Open Metrics

### 1. Prometheus-compatible API
- Prometheus API can be used through a Prometheus-compatible API.

[URL]

```http
[GET,POST,PUT,DELETE] /prometheus/{prometheus-api-endpoint}
Content-Type: application/json
```

#### Request

[Request Header]

| Header name | Value | Note|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | projectAppkeyCan check from the URL & Appkey in the top right section of Compute > System Monitoring |

```
curl "https://kr1-api-sysmon.cloud.toast.com/prometheus/api/v1/series?match[]=query&start=1621894796&end=1621905566" -v -H'x-tc-app-key:appkey'
```

#### Results

```
{
    "status": "success",
    "data": [
        {
            "__name__": "name",
            "domainname": "(none)",
            "instance": "instance",
            "job": "job",
            "machine": "x86_64",
            "nodename": "nodename",
            "openmetrics_id": "uuid",
            "release": "3.10.0-1127.19.1.el7.x86_64",
            "sysname": "Linux",
            "version": "#1 SMP Tue Aug 25 17:23:54 UTC 2020"
        },
        {
            "__name__": "name",
            "domainname": "(none)",
            "instance": "instance",
            "job": "job",
            "machine": "x86_64",
            "nodename": "nodename",
            "openmetrics_id": "uuid",
            "release": "3.10.0-1127.18.2.el7.x86_64",
            "sysname": "Linux",
            "version": "#1 SMP Sun Jul 26 15:27:06 UTC 2020"
        }
    ]
}
```

For more information, refer to [Prometheus HTTP API](https://prometheus.io/docs/prometheus/latest/querying/api/)

#### Available endpoint

| Metheod | endpoint |
| --- | --- |
| GET | /prometheus/api/v1/query |
| POST | /prometheus/api/v1/query |
| GET | /prometheus/api/v1/query_range |
| POST | /prometheus/api/v1/query_range |
| GET | /prometheus/api/v1/series |
| POST | /prometheus/api/v1/series |
| GET | /prometheus/api/v1/labels |
| POST | /prometheus/api/v1/labels |
| GET | /prometheus/api/v1/label/<label_name>/values |
| GET | /prometheus/api/v1/targets |
| GET | /prometheus/api/v1/rules |
| GET | /prometheus/api/v1/alerts |
| GET | /prometheus/api/v1/targets/metadata |
| GET | /prometheus/api/v1/metadata |

