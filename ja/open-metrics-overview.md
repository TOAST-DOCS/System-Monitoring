## Compute > System Monitoring > Advanced Monitoring(OpenMetrics) > 概要
**Compute > System Monitoring > Advanced Monitoring(OpenMetrics)**サービスは、ユーザーのインスタンスで動作する多様なプラットフォーム/アプリケーションのモニタリングを行うことができる拡張モニタリングツールです。
基本的なシステム指標の他にもユーザーの状況に応じてさまざまな指標を収集できる方法を紹介します。

## Prometheus紹介
* [Prometheus](https://prometheus.io/)はCNCF(Cloud Native Computing Foundation)のプロジェクトの中の1つで、システムとサービスをモニタリングするのに使われるツールです。
* Prometheusにモニタリング対象をHTTP URLで指定すると、Prometheusはそのパスにリクエストを送り、レスポンス値を元にモニタリング情報を収集します。
* 下記の方法で出力される[Prometheus説明形式](https://prometheus.io/docs/instrumenting/exposition_formats/)の指標データを収集できます。
    * 指標抽出ツール(Exporter)をインストールするか、システム/プラットフォームが提供するツールを使用する方法
        * [Third-party exporters](https://prometheus.io/docs/instrumenting/exporters/#third-party-exporters)
        * [Software exposing Prometheus metrics](https://prometheus.io/docs/instrumenting/exporters/#software-exposing-prometheus-metrics)
    * 形式に合わせて指標を出力するプログラムを直接作成して、任意の指標を抽出する方法
        * [Client Libraries](https://prometheus.io/docs/instrumenting/clientlibs/#client-libraries)

## OpenMetricsの紹介
* [OpenMetrics](https://github.com/OpenObservability/OpenMetrics/blob/master/OpenMetrics.md)はPrometheus説明形式とこれを基盤にした統合システムで使用するために推進されている標準化作業です。
* System MonitoringでもOpenMetrics基盤のモニタリングツールを提供します。
* 一般的にPrometheusを構築してモニタリングを行うには追加でリソースを消費し、ネットワーク構成管理が必要です。
    * ![Prometheus](https://static.toastoven.net/prod_system_monitoring/console_guide/open-metrics-overview-1.png)
* System Monitoringでは、各インスタンス内で指標を抽出できるパスが準備されると、Agentが代わりに指標を収集し、ユーザーは別途サービスを構築することなくモニタリングツールを使用できます。
    * ![System Monitoring Advanced Monitoring(OpenMetrics)](https://static.toastoven.net/prod_system_monitoring/console_guide/open-metrics-overview-2.png)

## 提供機能
### OpenMetrics基盤のカスタム指標収集およびダッシュボード提供
**Compute > Instance**で作成したサーバーインスタンスでモニタリングしたい対象システムのExporterをインストールして実行すると、そのシステムの指標情報を収集できるようになります。
Exporterが準備できたら、System Monitoringサービスでモニタリング機能を有効化して収集された指標を照会できます。システム指標と同様にチャートを作成し、任意のレイアウトで配置できます。レイアウトを複数作成して目的に合わせて管理できます。またサーバー基本モニタリングと同じように、観察対象指標としきい値を指定してサービスの異常兆候を把握できます。設定した監視条件を満たす状況が発生すると、メールまたはSMSでユーザーにメッセージを送信できます。


### 指標収集周期および保管期間
OpenMetricsで収集された指標は1分単位で収集され、最大5年間保管されます。指標データは5分、30分、2時間、1日単位で集計されます。各集計単位で保障する保管期間は下記のとおりです。

集計単位|保管期間
---|---
1分|7日
5分|1か月
30分|6か月
2時間|2年
1日|5年
> 最大保管期間は今後変更される場合があります。その場合は別途会員に告知します。
