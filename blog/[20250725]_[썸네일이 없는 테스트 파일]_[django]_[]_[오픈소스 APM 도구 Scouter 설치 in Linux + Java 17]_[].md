# 오픈소스 APM 도구 Scouter 설치 방법

* 작업 환경: Rocky Linux + Java 17(openJDK)

```Shell
# dnf install
dnf -y update
dnf -y install sudo
dnf -y install procps
dnf -y install net-tools
dnf -y install file
dnf -y install wget
dnf -y install java-1.8.0-openjdk.x86_64
dnf -y install java-17-openjdk.x86_64
dnf -y install firewalld

# open port for scouter
sudo firewall-cmd --zone=public --add-port=6100/tcp --permanent
sudo firewall-cmd --zone=public --add-port=6100/udp --permanent

# open port for tomcat
sudo firewall-cmd --zone=public --add-port=8080/tcp --permanent
sudo firewall-cmd --zone=public --add-port=8009/tcp --permanent

# restart firewall
sudo firewall-cmd --reload

#####

# download scouter
wget https://github.com/scouter-project/scouter/releases/download/v2.20.0/scouter-all-2.20.0.tar.gz

# unzip scouter
tar xvfz /wms/scouter/scouter-all-2.20.0.tar.gz

#####

# set up env path
vi /etc/profile

# when it's 1.8
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.452.b09-2.el8.x86_64
export PATH=$PATH:$JAVA_HOME/jre/bin

# when it's 17
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-17.0.15.0.6-2.el8.x86_64
export PATH=$PATH:$JAVA_HOME/bin

# apply
source /etc/profile

#####

# set up agent
vi {scouter 설치 경로}/agent.host/conf/scouter.conf

### scouter host configruation sample
#net_collector_ip=127.0.0.1
#net_collector_udp_port=6100
#net_collector_tcp_port=6100
#cpu_warning_pct=80
#cpu_fatal_pct=85
#cpu_check_period_ms=60000
#cpu_fatal_history=3
#cpu_alert_interval_ms=300000
#disk_warning_pct=88
#disk_fatal_pct=92


## 01. Collector 서버 전송 설정

# Collector( 수집 ) 서버의 호스트 이름
obj_name = scouter_monitoring_system

# Collector( 수집 ) 서버의 IP 주소
net_collector_ip = 127.0.0.1

# Collector 서버의 UDP Port
net_collector_udp_port = 6100

# Collector 서버의 TCP Port
net_collector_tcp_port = 6100


## 02. CPU 알림 설정 옵션

# CPU 경고 임계치
cpu_warning_pct = 80

# CPU 오류 임계치
cpu_fatal_pct = 85

# CPU 감시주기( millisecond )
cpu_check_period_ms = 60000

# CPU 알림 누적 카운트
cpu_fatal_history = 3

# CPU 알림 주기
cpu_alert_interval_ms = 300000


## 03. Memory 알림 설정 옵션
mem_alert_enabled = true
mem_warning_pct = 80
mem_fatal_pct = 90


## 04. DISK 사용 알림 설정

# CPU 경고 임계치( % )
disk_warning_pct = 88

# CPU 경고 임계치( % )
disk_fatal_pct = 92


#####

# set up java application of agent
vi {scouter 설치 경로}/agent.java/conf/scouter.conf

### scouter java agent configuration sample
#obj_name=WAS-01
#net_collector_ip=127.0.0.1
#net_collector_udp_port=6100
#net_collector_tcp_port=6100
#hook_method_patterns=sample.mybiz.*Biz.*,sample.service.*Service.*
#trace_http_client_ip_header_key=X-Forwarded-For
#profile_spring_controller_method_parameter_enabled=false
#hook_exception_class_patterns=my.exception.TypedException
#profile_fullstack_hooked_exception_enabled=true
#hook_exception_handler_method_patterns=my.AbstractAPIController.fallbackHandler,my.ApiExceptionLoggingFilter.handleNotFoundErrorResponse
#hook_exception_hanlder_exclude_class_patterns=exception.BizException


# Collector( 수집 ) 서버의 호스트 이름
obj_host_name = scouter_monitoring_system

# Agnet( 감시 대상 ) 서버의 별칭 지정
obj_name = Agent-00

# Collector( 수집 ) 서버의 IP 주소
net_collector_ip = 127.0.0.1

# Collector( 수집 ) 서버의 UDP Port
net_collector_udp_port = 6100

# Collector( 수집 ) 서버의 TCP Port
net_collector_tcp_port = 6100


# 프로파일링 할 메서드 지정 가능 - 좀더 분석해볼것 -
# Hooking 하여 기록할 method의 pattern 정의
# hook_method_patterns = sample.mybiz.*Biz.*,sample.service.*Service.*

# XLog 정보에는 IP 정보가 포함되어 있는데 proxy 등을 경유하는 경우
# 사용자 IP를( x-forwarded-for 같은 ) http header에서 구해오도록 설정
# trace_http_client_ip_header_key = X-Forwarded-For

# Spring의 request mapping method의 parameter를 profiling 합니다.
# profile_spring_controller_method_parameter_enabled = true

# error로 마킹할 Exception class pattern을 지정합니다.
# 상속받은 Exception class의 이름까지 검색합니다.
# hook_exception_class_patterns = my.exception.TypedException
# profile_fullstack_hooked_exception_enabled = true
# hook_exception_handler_method_patterns = my.AbstractAPIController.fallbackHandler,my.ApiExceptionLoggingFilter.handleNotFoundErrorResponse
# hook_exception_hanlder_exclude_class_patterns = exception.BizException

#####

# run scouter host
cd /wms/scouter/agent.host
./host.sh

#####

# set up server
vi /wms/scouter/server/conf/scouter.conf

# Server ID( Collector( 수집 ) 서버의 별칭 지정  )
server_id = scouter_service

# Agent 제어 및 Service 포트( Default : TCP 6100 )
net_tcp_listen_port = 6100

# UDP 수신 포트( Default : 6100 )
net_udp_listen_port = 6100

# DataBase 저장경로( Default : ./database )
db_dir = ./database

# Log 저장경로( Default : ./logs )
log_dir = ./logs

### 확인 및 분석 필요 항목 ###
# 저장소 자동 삭제 여부
# mgr_purge_enabled = true

# 프로퍼티 데이터를 자동으로 지우는 디스크 사용량
# mgr_purge_disk_usage_pct = 80 

# 프로퍼티 데이터를 자동으로 지워지기전 유지되는 날짜수
# mgr_purge_profile_keep_days = 10

# xlog 점 데이터가 자동으로 지워지기전 유지되는 날짜수
# mgr_purge_xlog_keep_days = 30

# 각종 카운터(선그래프값) 가 자동으로 지워지기전에 유지되는 날짜수
# mgr_purge_counter_keep_days = 70

# specify java version for server
vi {scouter 설치 경로}/server/startup.sh
nohup /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.452.b09-2.el8.x86_64/jre/bin/java -Xmx1024m -classpath ./scouter-server-boot.jar scouter.boot.Boot ./lib > nohup.out &
nohup /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.352.b08-2.fc35.x86_64/jre/bin/java -Xmx1024m -classpath ./scouter-server-boot.jar scouter.boot.Boot ./lib > nohup.out & ###(mobyus dev server)
sleep 1
tail -100 nohup.out

# run server
cd {scouter 설치 경로}/server
./startup.sh

#####

# run client
상단 메뉴의 Collector > Management > Account > Add Account
admin 외 새 계정 추가

#####

# set scouter as configuration when running spring boot jar
sudo nohup /usr/bin/java -DSpring.profiles.active=local --javaagent:{scouter 설치 경로}/agent.java/scouter.agent.jar -Dscouter.config={scouter 설치 경로}/agent.java/conf/scouter.conf -Dobj_name=wms-dev -jar {jar 파일 경로}
```