## Compute > System Monitoring > API 가이드

### 기본 정보
http API Endpoint

| 리전 | 엔드포인트 |
| --- | --- |
| 한국(판교) 리전 | https://kr1-api-sysmon.cloud.toast.com |
| 한국(평촌) 리전 | https://kr2-api-sysmon.cloud.toast.com |
| 미국 리전 | https://us1-api-sysmon.cloud.toast.com |
| 일본 리전 |    https://jp1-api-sysmon.cloud.toast.com |

## Prometheus API

### 1. Prometheus 지표 조회 API
- Prometheus 지표 조회 API를 사용할 수 있습니다.

[URL]

```http
[GET,POST] /prometheus/{prometheus-api-endpoint}
Content-Type: application/json
```

#### 요청

[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |

```
curl "https://kr1-api-sysmon.cloud.toast.com/prometheus/api/v1/series?match[]=query&start=1621894796&end=1621905566" -v -H'X-TC-APP-KEY:appkey'
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

### 2. Grafana 연동
- Prometheus 지표 조회 API를 Grafana에 연동하여 사용할 수 있습니다

### 2.1 Grafana란

#### metric data를 시각화해서 보여주는 대쉬보드를 제공해주는 툴입니다. 

### 2.2 Grafana를 사용해봅시다

- Grafana를 설치 후 접속 로그인 합니다.
- Configuration -> Data sources로 접근합니다.
- 우측의 Add data source를 클릭합니다.
![Grafana](https://static.toastoven.net/prod_system_monitoring/console_guide/grafana_guide.png)
- Prometheus를 선택합니다.
- Prometheus를 선택한 창에서 차례대로 Name, URL, Header를 입력합니다.
- 이 때 URL은 api-gateway의 주소 (ex: kr1-api-sysmon.cloud.toast.com) 에 prometheus api를 이용하기 위한 prefix (/prometheus)까지 입력합니다. (ex: https://kr1-api-sysmon.cloud.toast.com/prometheus) 
- Header값에는 key로 x-tc-app-key를, Value에는 SystemMonitoring상품의 appkey를 넣습니다. (Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다)
- 맨 하단의 Save & test버튼을 누르고 Data source is working이 정상적으로 뜨는지 확인합니다.
- 메인화면으로 돌아가면 목록에 새로 만든 datasource가 추가된 것을 확인할 수 있습니다.



## OpenMetrics 대시보드 작업공간 API
- API를 통해 OpenMetrics 대시보드의 작업공간 조회/생성/수정/삭제를 할 수 있습니다

#### 공통 에러 코드
| response code | 설명|
| --- | --- |
| 401 | Appkey 입력을 안 했거나 유효하지 않은 Appkey을 입력하셨습니다  |
| 403 | 접근이 불가능한 Project에 접근 시도하셨습니다       |

### 1. OpenMetrics 대시보드 작업공간 전체 조회

[URL]
```http
[GET] /v1.0/projects/{projectId}/jobs
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |

```
curl -i -X GET \
   -H "X-TC-APP-KEY:appkey" \
 'https://kr1-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs'
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

### 2. OpenMetrics 대시보드 작업공간 생성

[URL]
```http
[POST] /v1.0/projects/{projectId}/jobs
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |
| X-SYSMON-REGION | projectRegion | kr,kr2,us,jp  |
| Content-Type    | content Type  | application/json |

[Request Body]

| 키 | 값 | 비고|
| --- | --- | --- |
| jobName       | 작업공간 이름     |  |
| metricsPath   | 작업공간 URL 경로 |  |
| description   | 작업공간 설명     |  |  

[오류 코드]
| response code | resultCode | resultMessage         | 설명 |
| ---           | ---        | ---                   | --- |
| 200           |  -40001    | ALREADY_EXIST         | 입력한 값이 이미 존재합니다 |
| 200           |  -40002    | BAD_INPUT_VALUE       | API 입력값이 잘못되었습니다 |
| 200           |  -50000    | INTERNAL_SERVER_ERROR | 서버 에러가 발생하였습니다  |

```
curl -i -X POST \
   -H "X-TC-APP-KEY:appkey" \
   -H "X-SYSMON-REGION:kr" \
   -H "Content-Type:application/json" \
   -d \
   '{"jobName": "jobName",
   "metricsPath": "/metricPath", 
   "description": "description"
   } ' \
 'https://kr1-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs'
```

#### 결과
```
{
    "header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   "body":{
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

### 3. OpenMetrics 대시보드 작업공간 개별 조회

[URL]
```http
[GET] /v1.0/projects/{projectId}/jobs/{jobId}
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |

```
curl -i -X GET \
   -H "X-TC-APP-KEY:appkey" \
 'https://kr1-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs/{jobId}'
```

#### 결과
```
{
    "header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   "body":{
      "jobId": "jobId",
      "projectId": "projectId",
      "jobName": "jobName",
      "metricsPath": "/metricPath",
      "description": "description",
      "lstModifier": "lstModifier",
      "lstModYmdt": "2021-08-17T10:32:09",
      "reservedJobCd": null
   }
}
```

### 4. OpenMetrics 대시보드 작업공간 수정

[URL]
```http
[PUT] /v1.0/projects/{projectId}/jobs/{jobId}
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |
| Content-Type    | content Type  | application/json |

[Request Body]

| 키 | 값 | 비고|
| --- | --- | --- |
| metricsPath   | 작업공간 URL 경로 |  |
| description   | 작업공간 설명     |  |  

[오류 코드]
| response code | resultCode | resultMessage         | 설명 |
| ---           | ---        | ---                   | --- |
| 200           |  -40002    | BAD_INPUT_VALUE       | API 입력값이 잘못되었습니다 |
| 200           |  -40006    | NOT_FOUND_JOB         | 입력한 jobId가 없습니다   |
| 200           |  -50000    | INTERNAL_SERVER_ERROR | 서버 에러가 발생하였습니다   |

```
curl -i -X PUT \
   -H "X-TC-APP-KEY:appkey" \
   -H "Content-Type:application/json" \
   -d \
   '{
   "metricsPath": "/updatemetricsPath", 
   "description": "updatedescription"
   } ' \
 'https://kr1-api-sysmon.cloud.toast.com/v1.0/projects/aOpreudC/jobs/{jobId}'
```

#### 결과
```
{
   "header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   "body":{
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

### 5. OpenMetrics 대시보드 작업공간 삭제

[URL]
```http
[DELETE] /v1.0/projects/{projectId}/jobs/{jobId}?memberId=UUID
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |

[Query Parameter]

| 키 | 값 | 비고|
| --- | --- | --- |
| memberId   | UUID |  |

[오류 코드]
| response code | resultCode | resultMessage         | 설명 |
| ---           | ---        | ---                   | --- |
| 200           |  -40002    | BAD_INPUT_VALUE       | API 입력값이 잘못되었습니다 |
| 200           |  -40006    | NOT_FOUND_JOB         | 입력한 jobId가 없습니다    |
| 200           |  -50000    | INTERNAL_SERVER_ERROR | 서버 에러가 발생하였습니다   |

```
curl -i -X DELETE \
   -H "X-TC-APP-KEY:appkey" \
 'https://kr1-api-sysmon.cloud.toast.com/v1.0/projects/aOpreudC/jobs/{jobId}?memberId=UUID'
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

## OpenMetrics 대시보드 수집대상 API
- API를 통해 OpenMetrics 대시보드의 수집대상 조회/생성/삭제를 할 수 있습니다

#### 에러 코드
| response code | message | 설명|
| --- | --- | --- |
| 401 |     | Appkey 입력을 안 했거나 유효하지 않은 Appkey을 입력하셨습니다 |
| 403 |     | 접근이 불가능한 Project에 접근 시도하셨습니다        |

### 1. OpenMetrics 대시보드 수집대상 전체 조회

[URL]
```http
[GET] /v1.0/projects/{projectId}/jobs/{jobId}/targets
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |

```
 curl -i -X GET \
   -H "X-TC-APP-KEY:appkey" \
 'https://kr1-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs/{jobId}/targets

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

### 2. OpenMetrics 대시보드 수집대상 서버 조회

[URL]
```http
[GET] /v1.0/projects/{projectId}/servers
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |
| X-SYSMON-REGION | projectRegion | kr,kr2,us,jp  |

```
 curl -i -X GET \
   -H "X-TC-APP-KEY:appkey" \
   -H "X-SYSMON-REGION:kr" \
 'https://kr1-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/servers'

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
      "hostId": "hostId",
      "hostNm": "hostNm",
      "svrIp": "192.168.0.5",
      "projectId": "projectId",
      "instanceId": "instanceId"
      }
   ]
}
```

### 3. OpenMetrics 대시보드 수집대상 생성

[URL]
```http
[POST] /v1.0/projects/{projectId}/jobs/{jobId}/targets
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |
| Content-Type    | content Type  | application/json |

[Request Body]

| 키 | 값 | 비고|
| --- | --- | --- |
| hostId        | 작업공간 이름     | /v1.0/projects/{projectId}/servers로 조회한 호스트ID 입니다 |
| port          | 수집대상 PORT    |  |
| description   | 수집대상 설명     |  |  

[오류 코드]
| response code | resultCode | resultMessage         | 설명 |
| ---           | ---        | ---                   | --- |
| 200           |  -40002    | BAD_INPUT_VALUE       | API 입력값이 잘못되었습니다 |
| 200           |  -40004    | INVALID_HOST_OR_PROJECT | 입력한 hostId나 projectId가 잘못되었습니다 |
| 200           |  -40006    | NOT_FOUND_JOB         | 입력한 jobId가 없습니다   |
| 200           |  -50000    | INTERNAL_SERVER_ERROR | 서버 에러가 발생하였습니다   |

```
curl -i -X POST \
   -H "X-TC-APP-KEY:appkey" \
   -H "Content-Type:application/json" \
   -d \
   '{"description": "description",
   "hostId": "host id",
   "port": "post number"
   } ' \
 'https://kr1-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs/{jobId}'

```

#### 결과
```
{
   "header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   "body": "targetId"
}
```

### 4. OpenMetrics 대시보드 수집대상 개별 조회

[URL]
```http
[GET] /v1.0/projects/{projectId}/jobs/{jobId}/targets/{targetId}
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |

```
 curl -i -X GET \
   -H "X-TC-APP-KEY:appkey" \
 'https://kr1-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs/{jobId}/targets/{targetId}

```

#### 결과
```
{
    "header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   "body":{
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
}
```

### 5. OpenMetrics 대시보드 수집대상 삭제

[URL]
```http
[DELETE] /v1.0/projects/{projectId}/jobs/{jobId}/targets/{targetId}?memberId=UUID
```

#### 요청
[Request Header]

| 헤더 이름 | 값 | 비고|
| --- | --- | --- |
| X-TC-APP-KEY | projectAppkey | Compute > System Monitoring의 우측 상단 URL & Appkey에서 확인 가능합니다 |

[Query Parameter]

| 키 | 값 | 비고|
| --- | --- | --- |
| memberId   | UUID |  |

[오류 코드]
| response code | resultCode | resultMessage         | 설명 |
| ---           | ---        | ---                   | --- |
| 200           |  -40002    | BAD_INPUT_VALUE       | API 입력값이 잘못되었습니다  |
| 200           |  -40006    | NOT_FOUND_JOB         | 입력한 jobId가 없습니다     |
| 200           |  -40007    | NOT_FOUND_TARGET      | 입력한 targetId가 없습니다  |
| 200           |  -50000    | INTERNAL_SERVER_ERROR | 서버 에러가 발생하였습니다    |
```
curl -i -X DELETE \
   -H "X-TC-APP-KEY:appkey" \
 'https://kr1-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs/{jobId}/targets/{targetId}?memberId=UUID'

```

#### 결과
```
{
   "header":{
      "isSuccessful": true,
      "resultCode": 0,
      "resultMessage": "SUCCESS"
   },
   "body": "targetId"
}
```