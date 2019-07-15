## Compute > System Monitoring > 개요
`Compute > System Monitoring` 서비스에서는 `Compute > Instance`에서 사용자가 생성한 인스턴스에 대한 모니터링 기능을 제공합니다.
인스턴스의 시스템 리소스 상태를 차트 형태로 시각화해서 볼 수 있으며, 사용량에 임계치를 설정하여 특정 상태에 대한 알림을 이메일 또는 SMS로 받아볼 수 있습니다.

System Monitoring은 각 인스턴스 서버에 설치된 System Monitoring Agent를 통해서 시스템 지표를 수집힙니다.
때문에 별도의 Agent 설치 작업이 필요할 수 있습니다.

## 제공 기능
### 시스템 지표 대시보드 제공
`Compute > Instance`에서 생성한 서버 인스턴스의 각종 시스템 지표를 차트로 제공하여 각 서버의 상태를 파악할 수 있습니다. 시스템 지표 차트를 선택하여 원하는 레이아웃으로 배치할 수 있으며, 다수의 레이아웃을 생성하여 목적에 따라 관리할 수 있습니다.

시스템 지표는 1분 단위로 수집되며 최대 5년 동안 보관됩니다. 각 지표 데이터는 5분, 30분, 2시간, 1일 단위로 집계됩니다. 집계 단위별 보관 기간은 아래와 같습니다.

집계 단위|보관 기간
---|---
1분|7일
5분|1개월
30분|6개월
2시간|2년
1일|5년 

### 지표 감시 설정 및 알림
수집된 지표에 대해 임계치를 설정하여 서버를 상시 감시할 수 있습니다. 이를 통해 이상 징후를 파악할 수 있습니다. 
예를 들어, CPU 사용률이 90%를 넘는 경우, 특정 NIC의 사용량이 1000pps를 넘어서는 경우, 특정 프로세스가 중단되었는지 등 서버의 상태를 파악할 수 있는 다양한 감시 항목을 제공하고 있습니다.

### 통보 방법 선택: 이메일, SMS
설정한 감시 조건이 충족되는 상황 발생 시, 어떤 채널을 통해서 알림을 받을지 선택할 수 있습니다.
현재 이메일과 SMS을 지원하고 있습니다.

## 용어 설명
용어|설명
---|---
시스템 지표 | System Monitoring에서 수집하는 각 인스턴스의 리소스를 의미합니다. CPU 사용률, Load Average 1m, Memory 사용량 등이 있습니다.
레이아웃 | 시스템 지표 차트의 묶음입니다. 사용자가 원하는대로 차트를 배치할 수 있으며, 다수의 레이아웃을 생성하여 목적에 따라 관리할 수 있습니다.
사용자 그룹 | 이벤트 발생시 알림을 받을 사용자 목록입니다.
알림 그룹 | 임계치를 설정하고 어떤 인스턴스를 감시할 것인지, 이벤트 발생 시 어떤 사용자 그룹에 알림을 보낼 것인지를 지정합니다.
감시 설정 | 각 지표에 대한 임계치의 상세 설정을 의미합니다.