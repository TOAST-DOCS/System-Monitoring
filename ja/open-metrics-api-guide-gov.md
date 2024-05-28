## Monitoring > System Monitoring > APIガイド

### 基本情報

http API Endpoint

| リージョン | エンドポイント |
| --- | --- |
| 韓国 リージョン | https://gov-api-sysmon.cloud.toast.com |

## Prometheus API

### 1. Prometheus指標照会API
- Prometheus指標照会APIを使用できます。

[URL]

```http
[GET,POST] /prometheus/{prometheus-api-endpoint}
Content-Type: application/json
```

#### リクエスト

[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |

```
curl "https://gov-api-sysmon.cloud.toast.com/prometheus/api/v1/series?match[]=query&start=1621894796&end=1621905566" -v -H'x-tc-app-key:appkey'
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

### 2. Grafana連動
- Prometheus指標照会APIをGrafanaと連動して使用できます。

#### 2.1 Grafanaとは

- 指標データを視覚化して表示するダッシュボードを提供するツールです。

#### 2.2 Grafana使用方法

- Grafanaをインストールした後、ログインします。
- Configuration -> Data sourcesにアクセスします。
- 右側のAdd data sourceをクリックします。
- Prometheusを選択します。
![Grafana](https://static.toastoven.net/prod_system_monitoring/console_guide/grafana_guidefile.png)
- Prometheusを選択したウィンドウでName、URL、Headerを順番に入力します。
- この時、URLはAPI Gatewayのアドレス(例：gov-api-sysmon.cloud.toast.com)にPrometheus APIを利用するためのprefix(/prometheus)まで入力します。 (例：https://gov-api-sysmon.cloud.toast.com/prometheus) 
- Header値にはkeyでx-tc-app-keyを、ValueにはSystem Monitoring商品のappkeyを入れます。(Monitoring > System Monitoringの右上のURL & Appkeyで確認できます。)
- 一番下のSave & testボタンを押して"Data source is working"が正常に表示されるか確認します。
- メイン画面に戻ると、リストに新たに作成したdata sourceが追加されていることを確認できます。



## OpenMetricsダッシュボードワークスペースAPI
- APIを使用してOpenMetricsダッシュボードのワークスペースを照会、作成、修正、削除できます。

#### 共通エラーコード
| response code | 説明|
| --- | --- |
| 401 | Appkeyが入力されていないか、入力されたAppkeyが有効ではありません。  |
| 403 | アクセスができないProjectにアクセスを試みました。      |

### 1. OpenMetricsダッシュボードワークスペース全体照会

[URL]
```http
[GET] /v1.0/projects/{projectId}/jobs
```

#### リクエスト
[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |
| X-SYSMON-REGION | regionCode    | O | 照会したいregionのコードを入力します。(kr) |

```
curl -i -X GET \
   -H "X-TC-APP-KEY:appkey" \
   -H "X-SYSMON-REGION:kr" \
 'https://gov-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs'
```

#### レスポンス

| キー | 説明|
| --- | --- |
| header.isSuccessful   | API呼び出し成否 | 
| header.resultCode     | API呼び出し結果コード |
| header.resultMessage  | API呼び出し結果メッセージ|  
| body[].jobId          | ワークスペースID      | 
| body[].projectId      | プロジェクトID      |
| body[].jobName        | ワークスペース名   |  
| body[].metricsPath    | ワークスペースのURLパス | 
| body[].description    | ワークスペースの説明   |
| body[].lstModifier    | 最終修正者UUID   |  
| body[].lstModYmdt     | 最終修正日時    |  
| body[].reservedJobCd  | ワークスペース作成タイプ(nullの場合、ユーザーが直接作成)  |  

[例]
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

### 2. OpenMetricsダッシュボードワークスペース作成

[URL]
```http
[POST] /v1.0/projects/{projectId}/jobs
```

#### リクエスト
[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |
| X-SYSMON-REGION | regionCode    | O | ワークスペースを作成したいregionのコードを入力します。(kr) |
| Content-Type    | content Type  | O | application/json |

[Request Body]

| キー | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| jobName       | ワークスペース名   | O |  |
| metricsPath   | ワークスペースのURLパス | O |  |
| description   | ワークスペースの説明   |   |  |  

[エラーコード]

| response code | resultCode | resultMessage         | 説明 |
| ---           | ---        | ---                   | --- |
| 200           |  -40001    | ALREADY_EXIST         | 入力した値がすでに存在します。 |
| 200           |  -40002    | BAD_INPUT_VALUE       | API入力値が無効です。 |
| 200           |  -50000    | INTERNAL_SERVER_ERROR | サーバーエラーが発生しました。  |

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
 'https://gov-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs'
```

#### レスポンス

| キー | 説明|
| --- | --- |
| header.isSuccessful  | API呼び出し成否 | 
| header.resultCode    | API呼び出し結果コード |
| header.resultMessage | API呼び出し結果メッセージ|  
| body.jobId           | 作成されたワークスペースID      | 
| body.projectId       | プロジェクトID      |
| body.jobName         | 作成されたワークスペース名   |  
| body.metricsPath     | 作成されたワークスペースのURLパス | 
| body.description     | 作成されたワークスペースの説明   |
| body.lstModifier     | 最終修正者UUID   |  
| body.lstModYmdt      | 最終修正日時    |  
| body.reservedJobCd   | ワークスペース作成タイプ(nullの場合、ユーザーが直接作成)  |  

[例]
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

### 3. OpenMetricsダッシュボードワークスペース個別照会

[URL]
```http
[GET] /v1.0/projects/{projectId}/jobs/{jobId}
```

#### リクエスト
[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |

```
curl -i -X GET \
   -H "X-TC-APP-KEY:appkey" \
 'https://gov-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs/{jobId}'
```

#### レスポンス

| キー | 説明|
| --- | --- |
| header.isSuccessful  | API呼び出し成否 | 
| header.resultCode    | API呼び出し結果コード |
| header.resultMessage | API呼び出し結果メッセージ|  
| body.jobId           | ワークスペースID      | 
| body.projectId       | プロジェクトID      |
| body.jobName         | ワークスペース名   |  
| body.metricsPath     | ワークスペースのURLパス | 
| body.description     | ワークスペースの説明   |
| body.lstModifier     | 最終修正者UUID   |  
| body.lstModYmdt      | 最終修正日時    |  
| body.reservedJobCd   | ワークスペース作成タイプ(nullの場合、ユーザーが直接作成)  |  

[例]
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

### 4. OpenMetricsダッシュボードワークスペース修正

[URL]
```http
[PUT] /v1.0/projects/{projectId}/jobs/{jobId}
```

#### リクエスト
[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |
| Content-Type    | content Type  | O | application/json |

[Request Body]

| キー | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| metricsPath   | ワークスペースのURLパス | O |  |
| description   | ワークスペースの説明   |   |  |

[エラーコード]

| response code | resultCode | resultMessage         | 説明 |
| ---           | ---        | ---                   | --- |
| 200           |  -40002    | BAD_INPUT_VALUE       | API入力値が無効です。 |
| 200           |  -40006    | NOT_FOUND_JOB         | 入力したjobIdがありません。   |
| 200           |  -40012    | SYSTEM_RESERVED_JOB   | 基本ワークスペースは修正できません。 |
| 200           |  -50000    | INTERNAL_SERVER_ERROR | サーバーエラーが発生しました。  |

```
curl -i -X PUT \
   -H "X-TC-APP-KEY:appkey" \
   -H "Content-Type:application/json" \
   -d \
   '{
   "metricsPath": "/updatemetricsPath", 
   "description": "updatedescription"
   } ' \
 'https://gov-api-sysmon.cloud.toast.com/v1.0/projects/aOpreudC/jobs/{jobId}'
```

#### レスポンス

| キー | 説明|
| --- | --- |
| header.isSuccessful  | API呼び出し成否 | 
| header.resultCode    | API呼び出し結果コード |
| header.resultMessage | API呼び出し結果メッセージ|  
| body.jobId           | ワークスペースID      | 
| body.projectId       | プロジェクトID      |
| body.jobName         | ワークスペース名   |  
| body.metricsPath     | 修正されたワークスペースのURLパス | 
| body.description     | 修正されたワークスペースの説明   |
| body.lstModifier     | 最終修正者UUID   |  
| body.lstModYmdt      | 最終修正日時    |  
| body.reservedJobCd   | ワークスペース作成タイプ(nullの場合、ユーザーが直接作成)  |  

[例]
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

### 5. OpenMetricsダッシュボードワークスペース削除

[URL]
```http
[DELETE] /v1.0/projects/{projectId}/jobs/{jobId}
```

#### リクエスト
[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |

[エラーコード]

| response code | resultCode | resultMessage         | 説明 |
| ---           | ---        | ---                   | --- |
| 200           |  -40006    | NOT_FOUND_JOB         | 入力したjobIdがありません。   |
| 200           |  -40012    | SYSTEM_RESERVED_JOB   | 基本ワークスペースは削除できません。 |
| 200           |  -50000    | INTERNAL_SERVER_ERROR | サーバーエラーが発生しました。   |

```
curl -i -X DELETE \
   -H "X-TC-APP-KEY:appkey" \
 'https://gov-api-sysmon.cloud.toast.com/v1.0/projects/aOpreudC/jobs/{jobId}'
```

#### レスポンス

| キー | 説明|
| --- | --- |
| header.isSuccessful  | API呼び出し成否 | 
| header.resultCode    | API呼び出し結果コード |
| header.resultMessage | API呼び出し結果メッセージ|  
| body                 | 削除されたワークスペースID | 

[例]
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

## OpenMetricsダッシュボード収集対象API
- APIを使用してOpenMetricsダッシュボードの収集対象を照会、作成、削除できます。

#### エラーコード
| response code | message | 説明|
| --- | --- | --- |
| 401 |     | Appkeyが入力されていないか、入力されたAppkeyが有効ではありません。 |
| 403 |     | アクセスができないProjectにアクセスを試みました。       |

### 1. OpenMetricsダッシュボード収集対象全体照会

[URL]
```http
[GET] /v1.0/projects/{projectId}/jobs/{jobId}/targets
```

#### リクエスト
[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |

```
 curl -i -X GET \
   -H "X-TC-APP-KEY:appkey" \
 'https://gov-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs/{jobId}/targets

```

#### レスポンス

| キー | 説明|
| --- | --- |
| header.isSuccessful   | API呼び出し成否 | 
| header.resultCode     | API呼び出し結果コード |
| header.resultMessage  | API呼び出し結果メッセージ|  
| body[].targetId       | 収集対象ID      | 
| body[].jobId          | ワークスペースID      | 
| body[].hostId         | 収集対象ホストID | 
| body[].port           | 収集対象ポート番号 | 
| body[].resultCd       | 収集対象接続結果コード| 
| body[].failReason     | 収集対象接続失敗理由| 
| body[].mntrnStatCd    | 収集対象モニタリングステータスコード| 
| body[].lstModifier    | 最終修正者UUID   |  
| body[].lstModYmdt     | 最終修正日時    |  
| body[].hostNm         | 収集対象の名前   |  
| body[].svrIp          | 収集対象IP      |  

[例]
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

### 2. OpenMetricsダッシュボード収集対象サーバー照会

[URL]
```http
[GET] /v1.0/projects/{projectId}/servers
```

#### リクエスト
[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |
| X-SYSMON-REGION | regionCode    | O | 照会したいregionのコードを入力します。(kr) |

```
 curl -i -X GET \
   -H "X-TC-APP-KEY:appkey" \
   -H "X-SYSMON-REGION:kr" \
 'https://gov-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/servers'

```

#### レスポンス

| キー | 説明|
| --- | --- |
| header.isSuccessful   | API呼び出し成否 | 
| header.resultCode     | API呼び出し結果コード |
| header.resultMessage  | API呼び出し結果メッセージ|  
| body[].hostId        | ホストID        | 
| body[].hostNm        | ホスト名     | 
| body[].projectId     | プロジェクトID      | 
| body[].svrIp         | サーバーIP        | 
| body[].instanceId    | インスタンスID       | 

[例]
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

### 3. OpenMetricsダッシュボード収集対象作成

[URL]
```http
[POST] /v1.0/projects/{projectId}/jobs/{jobId}/targets
```

#### リクエスト
[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |
| Content-Type    | content Type  | O | application/json |

[Request Body]

| キー | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| hostId        | 収集対象に追加するホストID| O | /v1.0/projects/{projectId}/serversで照会したホストIDです。 |
| port          | 収集対象PORT    | O |  |

[エラーコード]

| response code | resultCode | resultMessage         | 説明 |
| ---           | ---        | ---                   | --- |
| 200           |  -40002    | BAD_INPUT_VALUE       | API入力値が無効です。 |
| 200           |  -40004    | INVALID_HOST_OR_PROJECT | 入力したhostIdまたはprojectIdが無効です。 |
| 200           |  -40006    | NOT_FOUND_JOB         | 入力したjobIdがありません。   |
| 200           |  -40012    | SYSTEM_RESERVED_JOB   | 基本ワークスペースには追加できません。 |
| 200           |  -50000    | INTERNAL_SERVER_ERROR | サーバーエラーが発生しました。   |

```
curl -i -X POST \
   -H "X-TC-APP-KEY:appkey" \
   -H "Content-Type:application/json" \
   -d \
   '{"hostId": "host id",
   "port": "post number"
   } ' \
 'https://gov-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs/{jobId}'

```

#### レスポンス

| キー | 説明|
| --- | --- |
| header.isSuccessful | API呼び出し成否 | 
| header.resultCode   | API呼び出し結果コード |
| header.resultMessage| API呼び出し結果メッセージ|  
| body                | 作成された収集対象ID | 

[例]
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

### 4. OpenMetricsダッシュボード収集対象個別照会

[URL]
```http
[GET] /v1.0/projects/{projectId}/jobs/{jobId}/targets/{targetId}
```

#### リクエスト
[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |

```
 curl -i -X GET \
   -H "X-TC-APP-KEY:appkey" \
 'https://gov-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs/{jobId}/targets/{targetId}

```

#### レスポンス

| キー | 説明|
| --- | --- |
| header.isSuccessful | API呼び出し成否 | 
| header.resultCode   | API呼び出し結果コード |
| header.resultMessage| API呼び出し結果メッセージ|  
| body.targetId       | 収集対象ID      | 
| body.jobId          | ワークスペースID      | 
| body.hostId         | 収集対象ホストID | 
| body.port           | 収集対象ポート番号 | 
| body.resultCd       | 収集対象接続結果コード| 
| body.failReason     | 収集対象接続失敗理由|
| body.mntrnStatCd    | モニタリングステータスコード  | 
| body.lstModifier    | 最終修正者UUID   |  
| body.lstModYmdt     | 最終修正日時    |  
| body.hostNm         | 収集対象の名前   |  
| body.svrIp          | 収集対象IP      |  

[例]
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

### 5. OpenMetricsダッシュボード収集対象削除

[URL]
```http
[DELETE] /v1.0/projects/{projectId}/jobs/{jobId}/targets/{targetId}
```

#### リクエスト
[Request Header]

| ヘッダ名 | 値 | 必須 | 備考|
| --- | --- | --- | --- |
| X-TC-APP-KEY    | projectAppkey | O | Monitoring > System Monitoringの右上にあるURL & Appkeyで確認可能 |

[エラーコード]

| response code | resultCode | resultMessage         | 説明 |
| ---           | ---        | ---                   | --- |
| 200           |  -40006    | NOT_FOUND_JOB         | 入力したjobIdがありません。     |
| 200           |  -40007    | NOT_FOUND_TARGET      | 入力したtargetIdがありません。  |
| 200           |  -40012    | SYSTEM_RESERVED_JOB   | 基本ワークスペースで削除できません。 |
| 200           |  -50000    | INTERNAL_SERVER_ERROR | サーバーエラーが発生しました。    |

```
curl -i -X DELETE \
   -H "X-TC-APP-KEY:appkey" \
 'https://gov-api-sysmon.cloud.toast.com/v1.0/projects/{projectId}/jobs/{jobId}/targets/{targetId}'

```

#### レスポンス

| キー | 説明|
| --- | --- |
| header.isSuccessful | API呼び出し成否 | 
| header.resultCode   | API呼び出し結果コード |
| header.resultMessage| API呼び出し結果メッセージ|  
| body                | 削除された収集対象ID | 

[例]
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
