## Monitoring > System Monitoring > 概要
**Monitoring > System Monitoring**服务提供针对用户在**Instance**中创建的实例的监控功能。
可以通过视觉化的图表形式视觉化查看实例的系统源状态，也可通过设置使用量临界值，以邮件或SMS接收特定状态的警报。

System Monitoring通过各实例服务器中安装的System Monitoring Agent收集系统指标。 
Agent默认包含在实例的映射中，因此实例驱动时自动开始收集。
但对于在推出System Monitoring服务的2019年7月23日之前创建且在运行中的实例，需要另行安装Agent。
Agent安装方法请参考**Monitoring > System Monitoring > 控制台指南 > Agent安装方法**。

## 提供功能
### 提供系统指标仪表板
以图表提供在**Compute > Instance**中创建的服务器实例的各种系统指标，可以掌握各服务器的状态。可选择系统指标图表按照所需布局进行排列，也可创建多个布局按照目的进行管理。

系统指标以1分钟为单位收集，最多保管5年。指标数据以5分钟、30分钟、2小时、1天为单位统计。各统计单位保存期限如下。

统计单位|保存期限
---|---
1分钟|7天
5分钟|1个月
30分钟|6个月
2小时|2年
1天|5年

### 指标监控设置及警报
可设置收集的指标的临界值，随时监控服务器，掌握异常征兆。
例如，提供CPU使用率超过90%、特定NIC的使用量超过1000pps、特定流程中断等情况下，提供用于掌握服务器状态的各种监控项目。

### 选择通知方法：邮件、SMS
可符合设置的监控条件的状况出现时，可以选择以何种方法接收警报。
可以通过邮件或SMS接收警报。

## 用语说明
用语|说明
---|---
系统指标 | System Monitoring收集的各实例的源。有CPU使用率、平均负载(load average) 1m、内存使用量等。
布局 | 系统指标图表的集合。可按照用户需要排列图表，可创建多个布局按照目的进行管理。
用户组 | 发生事件时接收警报的用户列表。
警报组 | 设置临界值并指定监控哪个实例、发生事件时向哪个用户组发送警报。
监控设置 | 各指标临界值的具体设置。
