💻 [AWS] CloudWatch
==================
# 💡 AWS CloudWatch 

* AWS 서비스의 리소스나 AWS 서비스 위에서 실행되고 있는 애플리케이션의 상태(EC2 인스턴스에서 운영중인 웹서버 등)를 **실시간으로 감시**할 수 있는 서비스
* 측정 대상의 지표(CPU 사용률, 메모리 사용률, 디스크 여유 공간 등)를 수집하고 측정 대상의 상태를 감시 및 관리 가능
* 대시보드를 생성하고 커스터마이징해서 사용자가 확인하고자 하는 지표들을 따로 선택하여 모니터링 가능
* 지표에 대해 기준치(임계값)를 설정하고 임계값을 초과하거나 미달할 경우 경보를 발생시켜 사용자가 알람을 받을 수 있도록 설정 가능


## 📌 CloudWatch 동작 방식

![](https://images.velog.io/images/dustjs159/post/5a76f9a1-7fb9-4e59-924f-196e26f5f652/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-17%2019.27.42.png)

* CloudWatch는 지표에 대한 측정 데이터 Repository
* EC2, RDS 등 AWS 서비스들의 지표에 대한 측정 데이터를 저장하고 저장한 데이터를 바탕으로 통계화 가능 
* 임계값을 설정하고 임계값을 초과하거나 미달인 경우 알람을 수신받고 이후에 진행할 작업을 설정해서 대비책 마련 가능
  * EC2 인스턴스를 종료, 중지, 재부팅의 작업 설정 가능
  * Auto Scaling 작업을 설정해서 인스턴스의 수를 늘리거나 줄일 수 있음

### ✔️ CloudWatch가 측정 대상을 감시하고 측정 데이터를 가져오는 방법


<img src="https://images.velog.io/images/dustjs159/post/a6570b1e-51b6-4b53-a429-ece4b0a46eef/image.png" width="75%">

* 측정 데이터는 **최대 15개월까지만 보관**
* Basic Monitoring : AWS의 System(H/W, Physical Machine 등 물리적인 장비의 개념? 이라고 보면 될 듯 합니다.)이 CloudWatch로 데이터를 전송
  * CloudWatch를 통해 확인할 수 있는 측정 데이터들중 AWS System을 확인하여 수집이 가능한 데이터들이 있음 → **default metric**
  * EC2 인스턴스의 경우 **5분 주기**로 측정 데이터를 CloudWatch에 전송
  * **요금 무료**
  * EC2 인스턴스의 namespace(AWS/EC2)에 포함된 default metric
    * ``CPUUtilization`` : 인스턴스의 CPU 사용률
    * ``NetworkIn/Out`` : 인스턴스에 대한 네트워크 I/O Bound Bytes
    * ``NetworkPacketsIn/Out`` : 인스턴스에 대한 네트워크 I/O Bound 패킷
    * ``StatusCheckFailed_System/Instance`` : 시스템/인스턴스의 상태 체크
    * ``EBSRead/WriteOps`` : 인스턴스의 EBS 볼륨 Read/Write 작업 성능

* Detailed Monitoring : CloudWatch Agent 를 설치하고 내부 수준(Detail) 데이터를 CloudWatch로 데이터를 전송
  * 인스턴스 내부 수준의 Detail한 데이터들은 AWS System을 감시하는 것으로는 확인이 불가능 하기 때문에 인스턴스 내부에 별도의 CloudWatch Agent를 설치하고 내부의 Agent가 CloudWatch로 데이터 전송
  * 설치한 Agent는 보다 더 Detail한 데이터(Memory Usage, Disk Usage 등)를 수집하고 CloudWatch로 측정 데이터를 전송
  * EC2 인스턴스의 경우 **1분 주기**로 측정 데이터를 CloudWatch로 전송
  * 별도의 Agent 설치 과정이 필요하며 **비용이 발생**

|구분|Basic Monitoring|Detailed Monitoring|
|------|---|---|
|Agent 설치 여부|X|O|
|비용|무료|유료|
|수집 주기|5분|1분 이내|

## 📌 CloudWatch 용어

![](https://images.velog.io/images/dustjs159/post/656dc66a-3b03-485c-8f8b-afddac0445a2/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-18%2009.08.58.png)

* Namespace
  * CloudWatch에 게시할 데이터들이 포함되어 있는 Container
  * AWS Namespace : AWS/``Service Name``
     * Ex) AWS/``EC2``, AWS/``RDS``
   * Custom Namespace
     * Ex) CWAgent, Collectd 
* **Metrics**
  * **지표**
  * 시간의 흐름에 따라 변화하는 **측정 데이터를 게시할 수 있는 지표**
    * Ex) EC2 의 인스턴스에 대한 ``CPUUtilization``
  * Metric 보존 기간
    * 측정 데이터에 대한 모니터링 주기(기간)가 60초 미만인 경우 3시간 동안의 측정 데이터만 확인 가능
    * 모니터링 주기가 1분 : 15일
    * 모니터링 주기가 5분 : 63일
    * 모니터링 주기가 1시간 : 15개월
    * 보존 기간(15개월)이 지난 데이터는 삭제
  ![](https://images.velog.io/images/dustjs159/post/d13a4a17-711e-4dc1-b993-732010519de3/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-28%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.25.49.png)
  * Metric의 데이터에 대해 모니터링 하고자 하는 기간 설정 가능
    * 분/시간/일/주/월 단위로 설정이 가능하고 최대 15개월 동안의 데이터까지 확인 가능
    
* **Dimensions**

  * **차원**
  * Metrics를 구별하기 위한 ``Name/Value`` Pair
  * 차원을 사용하여 Metric 데이터들 중 모니터링 하고자 하는 대상들만 필터링 할 수 있음
    * Ex) ``InstanceId="i-06ac2bb2633df9ebe"`` 인 대상의 Metric 데이터를 모니터링 하고자 할 때 ``InstanceId="i-06ac2bb2633df9ebe"`` 를 검색하여 특정 대상의 Metric 만을 모니터링 할 수 있음
    ![](https://images.velog.io/images/dustjs159/post/5f7cc37a-210d-4541-9d6d-e862817d2efa/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-28%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.38.00.png)
    
  * 차원을 검색할 때 검색 조건에 ``Name`` 같은 **Tag를 사용할 수 없음**
  
  ![](https://images.velog.io/images/dustjs159/post/980619a5-7b09-4eca-907e-e55d505e980b/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-28%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.40.47.png)

  * Dimension Combinations(차원 조합)
    * 여러 차원들을 조합하여 Metric 데이터 검색 가능 
    ``Dimensions: InstanceId="i-029bfece3fbebcc77" MetricName="CPUUtilization”``
    * 같은 차원의 조합은 중복이 불가능
    
![](https://images.velog.io/images/dustjs159/post/fceac0de-4843-45a9-b443-035d80619bfb/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-28%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.43.22.png)
    
* Resolution
  * Metric 데이터를 표시 할 간격
  * Standard(default)는 1분 간격, High는 1초 간격으로 표시
  * detail monitoring의 경우에만 High 설정이 가능하며 비용이 발생
* Statistics
  * Metric 데이터 집계 유형
  * Metric의 Period 동안의 측정 데이터를 어떻게 집계하여 표기할 것인지 선택
  * Average, Minimum, Maximum, Sum 등
* Periods
  * Metric에 표시할 데이터의 측정 기간
  * Metric에 Statistics 값을 띄워줄 Periods를 설정
    * Ex) 5분(Periods)동안의 평균(Statistics)
* Units
* Aggregation
* Percentiles
* Alarms


## 📌 CloudWatch 리소스


![](https://images.velog.io/images/dustjs159/post/fd3d581f-0b92-4898-ab40-8d130ebe320a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-24%2011.30.47.png)

* 경보(Alarm)
* 로그(Log)
* 지표(Metric)
* 이벤트(Event)
* 애플리케이션 모니터링(Application Monitoring)
