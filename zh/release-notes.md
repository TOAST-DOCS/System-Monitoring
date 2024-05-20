## Monitoring > System Monitoring > 릴리즈 노트

## 2024. 05. 28.
### 기능 개선/변경
* 서비스 카테고리 변경
  * Compute에서 Monitoring으로 카테고리가 변경되었습니다.

### 2023. 10. 31.

#### System Monitoring
* Bug Fixes
  * Fixed an issue that kept sending notifications to users excluded from projects

### 2023. 06. 27.

#### System Monitoring
* Fixed an issue where, when using the **Monthly Metrics Report**, excel files are not created intermittently
* Windows agent
  * Improved high availability feature
  * Added logs

### 2023. 04. 25.

#### System Monitoring
* Bug Fixes
  * Fixed an issue where downloaded monthly metrics reports intermittently fail to run

### 2023. 03. 28.

#### System Monitoring
* Removed the interval option `1m` in Monthly Metrics Report

### 2022. 07. 26.

#### System Monitoring
* Added a new feature: Monthly Metrics Report
  * Allows you to create and download monthly metric reports.
  * Allows you to create reports on metrics for up to 6 months on a monthly basis.
  * Among the Select Metrics items, `GENERAL` can be found in `Server Dashboard`, and `PROMQL` found in `OpenMetrics Dashboard`.
  * Each request can be found in `Monthly Metric Report`, and the report can be downloaded for a month after creation

### 2021. 12. 28.

#### System Monitoring
* Deleted the feature to add @Linux and @Windows default workspaces and deleted the created workspaces
  * @Linux and @Windows workspaces that were added automatically when creating an instance are no longer added automatically.
  * All @Linux and @Windows workspaces automatically created in the existing instances are deleted.

### 2021. 10. 26.

#### System Monitoring
* OpenMetrics Dashboard > Query
  * Changed to allow users to select only up to the date one year ago when selecting a query period.
  * Changed so that guide text regarding data unavailable status or errors is displayed in the chart
* OpenMetrics Dashboard > Add/Modify Charts
  * Changed so that, when the user clicks the **Add** button without selecting any metrics, guide text shows up and the location is highlighted.

### 2021. 09. 14.

#### System Monitoring
- Added new APIs: added APIs to view, add, or delete workspaces and collection targets
- Added @Linux, @Windows default workspaces
  - @Linux: Collects metrics of node exporter installed on an instance. When you create a Linux OS type instance, it is automatically added as the collection target of @Linux.
  - @Windows: Collects metrics of windows exporter installed on an instance. When you create a Windows OS type instance, it is automatically added as the collection target of @Windows.

### 2021. 07. 27.

#### System Monitoring

* Bug fixed: Fixed the problem of selecting ‘There are no entries.’ when adding server of notification group and user group.
* Bug fixed: Fixed the problem of creating more than 5 when creating advanced monitoring layout quickly
* Bug fixed: Fixed the problem of not being able to add other instances with same name to the same port as the collection target in **Advanced Monitoring > Workspace > Collection Target**

### 2021. 06. 29.

#### System Monitoring

* Improved OpenMetrics notification group input guide text
* Improved server/agent status tooltip size in server dashboard
* Fixed the problem in which some dropdown menu buttons were displayed abnormally on the event status screen
* Modified the instance name changed in **Compute > Instance** to be reflected in the server list on the server dashboard
* Modified loading bar
* Added API compatible to Prometheus (Beta)

### 2021. 01. 26.

#### System Monitoring
* Added new feature: Advanced Monitoring (OpenMetrics)
  * Provides the OpenMetrics (Prometheus exposition format) index collection, retrieval, and notification features

### 2020. 06. 23.

#### System Monitoring

* Updated chart and legend names to clarify
* Added detail indications on a chart for items with more details

### 2020. 02. 25.

#### System Monitoring
* Updates in Event Status Page
  * Updated to query events by each region
  * Added 'All' as status item for event search filters
  * Added the **Forced Stop** button, by which user can  directly close events
* Agent Updates
  * Optimized communication paths with System Monitoring servers
    * Indicators can be collected, regardless of internet gateway or security group settings
  * Upgraded usage volume for CPU and memory

### 2020. 01. 21.

#### System Monitoring
* Added Query Event Page
  * Query events occurred out of surveillance setup
* Updated **Server List** on Server Dashboard
  * Upgraded to query all instances in **Compute > Instance**
  * Updated to show instance status more precisely
* Updated **Server - User Integration** for Alarm Groups
  * Updated to save changes, by selecting a server and user group and clicking the save button

### 2019. 11. 26.

#### System Monitoring
##### Feature Updates

* Instance Search Updated on Server Dashboard: No distinction is required between upper and lower cases


### 2019. 10. 29.

#### System Monitoring
##### Feature Updates
- Updated UI for User Interactions
  - Updated to show the loading bar to search/add/modify/delete monitoring data, including user group, monitoring group, or monitoring setting.
  - Allowed to disable unnecessary buttons for interactions

##### Bug Fixes
- Fixed the error in the Japan and US region, where indicator collecting was temporarily suspended for servers with changed monitoring setting
- Fixed the issue of invalid output of dates for the adding/modifying user/monitoring groups, especially in the US region

### 2019. 09. 24.

#### System Monitoring
- Supports English for web console messages
- Fixed failure in the layout selection for server dashboard on Internet Explorer 11

### 2019. 08. 27.

#### System Monitoring
- Improved performance for the query of charts on server dashboard
- UI improved for the Internet Explorer 11 browser environment

### 2019. 07. 23.

#### Release of New Service: System Monitoring

- System metrics are provided on a chart for a newly created virtual server
- Each chart of system metrics can be configured under a layout of choice; you may set a notification to be sent to a group of particular users via email or SMS, when a metric reaches a specific threshold.
