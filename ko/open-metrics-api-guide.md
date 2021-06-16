## Compute > System Monitoring > API 가이드

### 기본 정보
```http
API Endpoint: https://kr1-api-sysmon.cloud.toast.com
```

## Open Metrics

### 1. Prometheus 호환 API
- Prometheus 호환 API를 통해 Prometheus API를 사용할 수 있습니다.

[URL]

```http
[GET,POST,PUT,DELETE] /prometheus/{prometheus-api-endpoint}
Content-Type: application/json
```

#### 요청

[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring 의 우측 상단 URL & Appkey에서 확인 가능 |

```
curl "http://kr1-api-sysmon.cloud.toast.com/prometheus/api/v1/query_range" -v -H'x-tc-app-key:appkey' -G --data-urlencode 'query=go_gc_duration_seconds' --data-urlencode 'start=2021-06-10T00:00:00Z' --data-urlencode 'end=2021-06-11T00:00:00Z' --data-urlencode 'step=10m'
```

#### 결과

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

상세한 내용은 <https://prometheus.io/docs/prometheus/latest/querying/api/> 참고 부탁드립니다.

#### 사용 가능한 endpoint

| Metheod | endpoint |
| --- | --- |
| GET | /api/v1/query |
| POST | /api/v1/query |
| GET | /api/v1/query_range |
| POST | /api/v1/query_range |
| GET | /api/v1/series |
| POST | /api/v1/series |
| GET | /api/v1/labels |
| POST | /api/v1/labels |
| GET | /api/v1/label/<label_name>/values |
| GET | /api/v1/targets |
| GET | /api/v1/rules |
| GET | /api/v1/alerts |
| GET | /api/v1/targets/metadata |
| GET | /api/v1/metadata |

