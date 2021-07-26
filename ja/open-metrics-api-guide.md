## Compute > System Monitoring > APIガイド

### 基本情報
```
http API Endpoint

https://kr1-api-sysmon.cloud.toast.com
https://kr2-api-sysmon.cloud.toast.com
https://us1-api-sysmon.cloud.toast.com
https://jp1-api-sysmon.cloud.toast.com
```

## Open Metrics

### 1. Prometheus互換API
- Prometheus互換APIを通してPrometheus APIを使用できます。

[URL]

```http
[GET,POST,PUT,DELETE] /prometheus/{prometheus-api-endpoint}
Content-Type: application/json
```

#### リクエスト

[Request Header]

| ヘッダ名前 | 値 | 備考|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoringの右上にあるURL & Appkeyで確認可能 |

```
curl "https://kr1-api-sysmon.cloud.toast.com/prometheus/api/v1/series?match[]=query&start=1621894796&end=1621905566" -v -H'x-tc-app-key:appkey'
```

#### 結果

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

詳細な内容は[Prometheus HTTP API](https://prometheus.io/docs/prometheus/latest/querying/api/)を参照してください。

#### 使用可能なendpoint

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
| GET | /prometheus/api/v1/label/\{label_name\}/values |
| GET | /prometheus/api/v1/metadata |
