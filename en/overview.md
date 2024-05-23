## Monitoring > System Monitoring > Overview
**Monitoring > System Monitoring** Service provides monitoring feature for the instances created by users in **Instance**.
You can view the system resource status of the instance in a chart form. You can set a usage threshold to receive a notification upon reaching a specific state via email or SMS.

System Monitoring collects system metrics to the System Monitoring Agent installed on each instance server. 
Since the Agent is included in the image of the instance by default, it starts collecting them when the instance is started.
However, for the instances which was created before July 23, 2019, which was the release date of System Monitoring service, an Agent should be installed separately.
To install the Agent, see **Monitoring > System Monitoring > Console Guide > How to Install Agent**.

## Provided Features
### System metric dashboard provided
It provides various system metrics of the server instances created in **Compute > Instance** as charts so that you can view the status of each server. You can select a System metric chart and display it as a layout of your choice and create / manage several layouts to fit the purpose.

The System metric is collected every minute and retained for up to 5 years. The metric data is aggregated every 5 min, 30 min, 2 hrs, or 1 day. The retention period per aggregation unit is as follows:

Aggregation Unit|Retention Period
---|---
1 minute|7 days
5 minutes|1 month
30 minutes|6 months
2 hours|2 years
1 day|5 years

### Metric Monitoring Setting and Notification
You can set thresholds for collected metrics, constantly monitor your server, and spot any abnormal symptoms of the server.
It provides various monitoring items to figure out the server status (e.g. the CPU usage is higher than 90%, the usage of a specific NIC exceeds 1000 pps, a specific process has been stopped).

### Select Notification Type: Email, SMS
You can select the type of method to receive a notification when a situation meets the monitoring conditions.
You can receive a notification via email or SMS.

## Terms Description
Terms|Description
---|---
System Metric | A resource of each instance collected by System Monitoring. This includes CPU usage, load average 1 m, and memory usage.
Layout | A bundle of System metric charts. User can place System metric charts as desired and   create and manage several layouts according to the purpose.
User Group | A list of users who will receive notifications when an event occurs.
Notify Group | Sets the threshold and specifies which instance will be monitored and to which user group a notification will be sent when an event occurs.
Monitoring Setting | A detailed setting of each metric threshold.

