## Compute > System Monitoring > API 가이드

### 기본 정보
http API Endpoint

| 리전 | 엔드포인트 |
| --- | --- |
| 한국(판교) 리전 | https://kr1-api-sysmon.cloud.toast.com |
| 한국(평촌) 리전 | https://kr2-api-sysmon.cloud.toast.com |
| 미국 리전 | https://us1-api-sysmon.cloud.toast.com |
| 일본 리전 |    https://jp1-api-sysmon.cloud.toast.com |

## Open Metrics

### 1. 지표 조회 API
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
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능 |

```
curl "https://kr1-api-sysmon.cloud.toast.com/prometheus/api/v1/series?match[]=query&start=1621894796&end=1621905566" -v -H'x-tc-app-key:appkey'
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

자세한 내용은 [Prometheus HTTP API](https://prometheus.io/docs/prometheus/latest/querying/api/)를 참고하시기 바랍니다.

#### 사용 가능한 endpoint

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


## OpenMetrics 작업공간 API
- API를 통해 OpenMetrics 대시보드의 작업공간 조회/생성/수정/삭제를 할 수 있습니다
### 1. OpenMetrics 작업공간 조회

[URL]
```http
[GET] /openmetric/projects/{projectId}/jobs
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능 |

```
curl -i -X GET \
   -H "x-tc-app-key:appkey" \
 'https://kr1-api-sysmon.cloud.toast.com/openmetric/projects/{projectId}/jobs'
```

#### 결과
```
{
    header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   body":[
      {
         "jobId": "jobId",
         "projectId": "projectId",
         "jobName": "jobName",
         "metricsPath": "/metricPath",
         "description": "description",
         "lstModifier": "lstModifier",
         "lstModYmdt": "2021-08-17T10:32:09",
         "reservedJobCd": null
      }
   ]
}
```

### 2. OpenMetrics 작업공간 생성

[URL]
```http
[POST] /openmetric/projects/{projectId}/jobs
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능 |
| X-Sysmon-Region | projectRegion | kr,k2,us,jp  |
| Content-Type    | content Type  | application/json |

[Request Body]

| 키 | 값 | 비고|
| --- | --- | --- |
| jobName       | 작업공간 이름     |  |
| metricsPath   | 작업공간 URL 경로 |  |
| description   | 작업공간 설명     |  |  

```
curl -i -X POST \
   -H "x-tc-app-key:appkey" \
   -H "X-Sysmon-Region:kr" \
   -H "Content-Type:application/json" \
   -d \
   '{"jobName": "jobName",
   "metricsPath": "/metricPath", 
   "description": "description"
   } ' \
 'https://kr1-api-sysmon.cloud.toast.com/openmetric/projects/{projectId}/jobs'
```

#### 결과
```
{
    header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   body":{
      "jobId": "jobId",
      "projectId": "projectId",
      "jobName": "jobName",
      "metricsPath": "/metricsPath",
      "description": "description",
      "lstModifier": null,
      "lstModYmdt": "2021-08-17T10:30:06",
      "reservedJobCd": null
   }
}
```

### 3. OpenMetrics 작업공간 수정

[URL]
```http
[PUT] /openmetric/projects/{projectId}/jobs/{jobId}
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능 |
| Content-Type    | content Type  | application/json |

[Request Body]

| 키 | 값 | 비고|
| --- | --- | --- |
| metricsPath   | 작업공간 URL 경로 |  |
| description   | 작업공간 설명     |  |  

```
curl -i -X PUT \
   -H "x-tc-app-key:appkey" \
   -H "Content-Type:application/json" \
   -d \
   '{
   "metricsPath": "/updatemetricsPath", 
   "description": "updatedescription"
   } ' \
 'https://kr1-api-sysmon.cloud.toast.com/openmetric/projects/aOpreudC/jobs/{jobId}'
```

#### 결과
```
{
   header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   body":{
      "jobId": "jobId",
      "projectId": "projectId",
      "jobName": "jobName",
      "metricsPath": "/updatemetricsPath",
      "description": "updatedescription",
      "lstModifier": null,
      "lstModYmdt": "2021-08-17T10:35:06",
      "reservedJobCd": null
   }
}
```

### 4. OpenMetrics 작업공간 삭제

[URL]
```http
[DELETE] /openmetric/projects/{projectId}/jobs/{jobId}?memberId=UUID
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능 |

[Query Parameter]

| 키 | 값 | 비고|
| --- | --- | --- |
| memberId   | UUID |  |

```
curl -i -X DELETE \
   -H "x-tc-app-key:appkey" \
 'http://localhost:8011/openmetric/projects/aOpreudC/jobs/{jobId}?memberId=UUID'
```

#### 결과
```
{
    "header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   "body": "jobId"
}
```

## OpenMetrics 수집대상 API
- API를 통해 OpenMetrics 대시보드의 수집대상 조회/생성/삭제를 할 수 있습니다
### 1. OpenMetrics 수집대상 조회

[URL]
```http
[GET] /openmetric/projects/{projectId}/jobs/{jobId}/targets
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능 |

```
 curl -i -X GET \
   -H "x-tc-app-key:appkey" \
 'https://kr1-api-sysmon.cloud.toast.com/openmetric/projects/{projectId}/jobs/{jobId}/targets

```

#### 결과
```
{
    "header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   "body":[
      {
         "targetId": "targetId",
         "jobId": "jobId",
         "hostId": "hostId",
         "port": 9100,
         "resultCd": 0,
         "failReason": null,
         "mntrnStatCd": null,
         "lstModifier": "lstModifier",
         "lstModYmdt": "2021-08-17T11:06:29",
         "hostNm": "hostNm",
         "svrIp": "192.168.0.5"
      }
   ]
}
```

### 2. OpenMetrics 수집대상 목록 조회

[URL]
```http
[GET] /openmetric/projects/{projectId}/servers
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능 |
| X-Sysmon-Region | projectRegion | kr,k2,us,jp  |

```
 curl -i -X GET \
   -H "x-tc-app-key:appkey" \
   -H "X-Sysmon-Region:kr" \
 'https://kr1-api-sysmon.cloud.toast.com/openmetric/projects/{projectId}/servers'

```

#### 결과
```
{
    header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   body":[
      {
      "hostId": "hostId",
      "hostNm": "hostNm",
      "svrIp": "192.168.0.5",
      "projectId": "projectId",
      "instanceId": "instanceId"
      }
   ]
}
```

### 3. OpenMetrics 수집대상 생성

[URL]
```http
[POST] /openmetric/projects/{projectId}/jobs/{jobId}/targets
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능 |
| Content-Type    | content Type  | application/json |

[Request Body]

| 키 | 값 | 비고|
| --- | --- | --- |
| hostId        | 작업공간 이름     | /openmetric/projects/{projectId}/servers로 조회한 호스트ID |
| port          | 수집대상 PORT    |  |
| description   | 수집대상 설명     |  |  

```
curl -i -X POST \
   -H "x-tc-app-key:appkey" \
   -H "Content-Type:application/json" \
   -d \
   '{"description": "description",
   "hostId": "host id",
   "port": "post number"
   } ' \
 'https://kr1-api-sysmon.cloud.toast.com/openmetric/projects/{projectId}/jobs/{jobId}'

```

#### 결과
```
{
    header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   body": "targetId"
}
```

### 4. OpenMetrics 수집대상 삭제

[URL]
```http
[DELETE] /openmetric/projects/{projectId}/jobs/{jobId}/targets/{targetId}?memberId=UUID
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능 |

[Query Parameter]

| 키 | 값 | 비고|
| --- | --- | --- |
| memberId   | UUID |  |

```
curl -i -X DELETE \
   -H "x-tc-app-key:appkey" \
 'https://kr1-api-sysmon.cloud.toast.com/openmetric/projects/{projectId}/jobs/{jobId}/targets/{targetId}?memberId=UUID'

```

#### 결과
```
{
    header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   body": "targetId"
}
```