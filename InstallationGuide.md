# 설치 가이드

### 공통 {#user-content-공통}

#### 회원 가입 {#user-content-회원-가입}

[![190](https://github.com/jinronara/deleteme_2/raw/master/images/190.png)](https://github.com/jinronara/deleteme_2/blob/master/images/190.png)

* 회사 계정, 회사 타이틀\(직급\), 이름, SMS인증, 회사명, 비밀번호, 회사 참조 코드\(옵션\)을 입력하여 회원가입을 진행합니다.
* 회원가입 완료 후 등록한 이메일로 가입 승인 안내 메일이 전송됩니다.
* 이메일을 확인하여 가입승인을 완료하면 와탭 계정이 생성 됩니다.

### Java 애플리케이션 모니터링 {#user-content-java-애플리케이션-모니터링}

#### 모니터링 에이전트 개요 {#user-content-모니터링-에이전트-개요}

와탭 Java 애플리케이션 모니터링 은 Java 기반 웹 애플리케이션 서버 모니터링 서비스를 제공합니다.

**에이전트 설치 방식 개요**

와탭은 사용자 편의를 위해 2가지 방식의 에이전트 설치 방식을 제공합니다.

사용자 애플리케이션 환경에 따라 “javaagent”, “javaagent+onetime attach” 방식 중 택일하여 에이전트를 설치 할 수 있습니다.

* 와탭은 애플리케이션 서버 기동 상태에서 최초 설치 시에는 attach 방식을 활용하고 재기동 이후 “javaagent” 방식을 활용하는 “javaagent+onetime attach” 방식을 권장합니다.
* IBM JDK의 경우 “watcher” 방식으로 에이전트를 실행시킬 경우 트랜잭션 정보가 수집되지 않으므로 “javaagent” 방식으로 에이전트를 실행해야 하는 제약이 있습니다.

**javaagent + onetime attach 방식**

애플리케이션 서버 부팅 시에 성능 데이터 수집을 위한 모듈을 주입하는 방식과 실행 중인 애플리케이션 서버에 모듈을 주입하는 방식을 혼용하는 방식입니다.

“javaagent” 방식과 동일한 설정을 실행중인 애플리케이션 서버의 실행 스크립트에 추가하여 애플리케이션 서버 재기동 시에도 모니터링 기능이 유지되도록 설정함과 동시에, 실행 중인 애플리케이션 서버에도 모니터링 기능을 활성화 합니다. attach.sh가 일회성으로 애플리케이션 서버 프로세스를 식별하고 Tracer를 활성화 합니다.

* 애플리케이션 서버 재기동에 민감한 환경에 APM 모니터링을 적용할 경우 유용한 방식이며, 애플리케이션 서버 재기동 이후에는 와탭의 권장 방식으로 모니터링이 수행되는 방식입니다.

[![200](https://github.com/jinronara/deleteme_2/raw/master/images/200.png)](https://github.com/jinronara/deleteme_2/blob/master/images/200.png)

* javaagent + onetime attach 적용법
  * 애플리케이션 서버 실행 스크립트에 JVM 옵션으로 -javaagent 옵션에 Tracer의 파일 경로를 추가합니다.
  * attach.sh을 실행하여 실행 중인 애플리케이션 서버에 Tracer를 활성화시킵니다.

**javaagent 방식**

애플리케이션 서버 부팅 시에 성능 데이터 수집을 위한 모듈을 주입하는 방식입니다.[![210](https://github.com/jinronara/deleteme_2/raw/master/images/210.png)](https://github.com/jinronara/deleteme_2/blob/master/images/210.png)

javaagent 적용법

* 애플리케이션 서버 실행 스크립트에 JVM 옵션으로 -javaagent 옵션에 Tracer의 파일 경로를 추가합니다.
* 애플리케이션 서버를 재기동 시 Tracer가 애플리케이션 서버의 하위 프로세스로 실행되어 성능 수집 코드를 주입합니다.
  * Tracer: 성능 데이터 수집을 위한 모듈

**구성 파일**

와탭 모니터링 에이전트는 모니터링 정보를 수집하여 서버에 전송하기 위한 Tracer와 “watcher” 방식 활용 시 Tracer를 애플리케이션에 attach하기 위한 Watcher 및 에이전트를 디버깅하기 위한 쉘 스크립트 파일로 구성됩니다.

와탭 모니터링 에이전트를 구성하는 각 파일의 역할은 다음과 같습니다.

**공통 구성 파일**

| 파일명 | 설명 |
| :--- | :--- |
| whatap.agent.tracer-\#.\#.\#.jar | Tracer - 웹 애플리케이션 서버 프로세스에 Attach되어 정보를 수집/서버로 전송하는 프로그램 |
| whatap.conf | 애플리케이션 서버의 데이터를 수집하는 수집서버의 주소와 서버의 프로젝트 라이선스 키가 입력되는 파일 |

**javaagent + onetime attach 실행 파일**

| 파일명 | 설명 |
| :--- | :--- |
| attach.sh\(bat\) | 실행 중인 애플리케이션 서버에 일회성으로 Tracer를 적용하기 위한 리눅스\(Windows\)계열 OS용 실행 쉘스크립트 |

**유틸리티 구성 파일**

| 파일명 | 설명 |
| :--- | :--- |
| javaproc.sh\(bat\) | 실행중인 자바 프로세스들의 PID와 JVM 옵션을 확인하는 리눅스\(Windows\)계열 OS용 실행 쉘스크립트 |
| resmon.sh\(bat\) | CPU/Memory/Disk 정보 추출을 위한 리눅스\(Windows\)계열 OS용 실행 쉘스크립트 |
| proxy.conf | 소프트웨어 프록시 설정 파일 |
| proxy.sh\(bat\) | 소프트웨어 프록시 실행을 위한 리눅스\(Windows\)계열 OS용 실행 쉘스크립트 |
| ping.sh\(bat\) | 서버와의 통신 확인을 위한 위한 리눅스\(Windows\)계열 OS용 실행 쉘스크립트 |

**에이전트 이름 식별**

와탭은 모니터링 정보 수집 대상인 애플리케이션 서버 식별을 위한 정보로 기본적으로 애플리케이션 서버로부터 수집한 정보를 활용합니다. 기본적으로 활용하는 정보는 애플리케이션 서버 종류, 애플리케이션 서버의 IP, 서비스 포트를 조합하여 애플리케이션 서버를 고유 식별자로 사용하게 되며 필요에 따라 사용자가 지정한 명칭을 사용하거나 패턴을 변경하여 사용하는 것도 가능합니다. 이때에는 꼭 고유한 값이어야만 합니다. 애플리케이션 서버로부터 추출한 정보를 활용하는 이유는 애플리케이션 서버의 정지, 단절 또는 에이전트 문제로 인한 수집 서버와 에이전트의 통신 단절 상태가 복구되었을 경우, 재 접속된 에이전트로부터 송신되는 정보가 기존 에이전트로부터 송신된 정보와의 연속성을 유지하기 위해서입니다. 와탭이 애플리케이션 서버를 식별하기 위해 사용하는 기본 패턴은 다음과 같습니다.

* default: {type}-{ip2}-{ip3}-{port}
* 마지막 요소가 {port}가 아닌 {pid}로 나올 경우 애플리케이션 서버의 서비스 포트가 인식되지 않은 것으로 애플리케이션의 마지막 항목에 표시되는 PID\(프로세스 ID\)를 참고하여 설치 문제에 대응합니다.

#### 에이전트 설치/실행/업데이트/중지 {#user-content-에이전트-설치-실행-업데이트-중지}

와탭 APM 모니터링 서비스를 사용하기 위해서는 모니터링 대상 애플리케이션 서버에 와탭 APM 모니터링 에이전트를 설치해야 합니다.

와탭 APM 모니터링 에이전트 설치 방법은 whatap.io 사이트에서 압축된 에이전트 파일을 다운로드 받아 서버 임의의 위치에 압축을 풀어 실행하는 것만으로 설치가 완료됩니다.

**공통**

**프로젝트 생성**

[![220](https://github.com/jinronara/deleteme_2/raw/master/images/220.png)](https://github.com/jinronara/deleteme_2/blob/master/images/220.png)

서버를 등록하기 위해 우선 프로젝트를 생성합니다. 추가 버튼을 선택하면 아래와 같이 프로젝트 생성 창이 나타납니다. PHP 아이콘을 선택한 뒤, 희망하는 프로젝트명과 데이터 서버 지역\(Region\), 소속하게 될 그룹을 선택한 뒤 프로젝트를 생성합니다.[![230](https://github.com/jinronara/deleteme_2/raw/master/images/230.png)](https://github.com/jinronara/deleteme_2/blob/master/images/230.png)

**라이선스 발급**

[![240](https://github.com/jinronara/deleteme_2/raw/master/images/240.png)](https://github.com/jinronara/deleteme_2/blob/master/images/240.png)

프로젝트 관리화면에서는 우선적으로 라이선스를 발급 받습니다. 라이선스 키는 프로젝트별로 귀속되기 때문에, 유출되거나 배포되어서는 안됩니다. 반드시 본인 프로젝트에 서버를 등록할 때에만 이용하시기 바랍니다.

**에이전트 다운로드**

[![250](https://github.com/jinronara/deleteme_2/raw/master/images/250.png)](https://github.com/jinronara/deleteme_2/blob/master/images/250.png)

라이선스를 발급 받은 후에는 ‘에이전트 파일 다운로드’ 버튼이 활성화 되었음을 확인할 수 있습니다. 해당 버튼을 눌러 와탭 에이전트 파일을 다운로드 받습니다.

다운로드가 완료되면 안에 있는 whatap.conf 파일의 설정을 확인하여 라이선스키와 데이터 수집 서버 주소가 정상적으로 들어가 있는지를 확인합니다.

```text
license={라이선스 키}
whatap.server.host={수집서버 정보}
```

* wget으로 직접 다운 받을 경우, whatap.conf 파일에 라이선스키와 데이터 수집 서버 주소가 정상적으로 들어가지 않습니다. 해당 방식으로 다운 받을 경우, 업로드 후 별도로 라이선스키와 데이터 수집 서버 주소를 넣어주시기 바랍니다.

**에이전트 업로드**

애플리케이션 서버가 설치된 서버에 접속하고, 다운로드 받은 에이전트 파일을 업로드 한 후, 압축해제를 합니다.

* $WHATAP\_HOME은 와탭 APM 모니터링 에이전트의 설치 경로를 가리키며, 이후 본 문서에서 이와 같이 기술합니다.
* 에이전트는 수집 서버 주소로 애플리케이션 서버의 성능 정보를 전송합니다. 그러므로 방화벽에 수집 서버 IP로의 TCP 아웃바운드 포트 \(6600\)이 차단되어 있으면 안됩니다.

**자원 수집 가능 여부 확인**

$WHATAP\_HOME 경로로 이동하여 CPU/Memory/Disk 정보 추출 가능 여부를 확인합니다.

```text
$ ./resmon.sh
_      ____   	______
| | /| / / /  ___ /_  __/__ ____
| |/ |/ / _ \/ _ `// / / _ `/ _ \
|__/|__/_//_/\_,_//_/  \_,_/ .__/
                     	     /_/
Just Tap, Always Monitoring
WhaTap Agent version 0.3.7 20161107
cpu      pcpu	mem 	disk
120322 14.06	0.0     42.0	85.0
120325 14.06	0.0     42.0	85.0
```

이후 절차는 각각의 설치 방식에 따라 진행하면 됩니다.

* 진행되는 절차가 상이하여 다른 작업 방식을 적용할 경우 에이전트가 정상적으로 작동되지 않을 수 있으니 반드시 본 매뉴얼을 참고해주시기 바랍니다.

**javaagent + onetime attach 방식**

실행 중 애플리케이션 서버에는 attach 방식으로 모니터링 기능을 적용하고, 애플리케이션 서버의 재기동 시점에 “javaagent” 방식을 적용합니다. 실행 상태의 애플리케이션 서버를 재기동 하지 않고 모니터링을 수행하고, 애플리케이션 서버 재기동 시에는 권장 설치 방식으로 모니터링 기능을 적용합니다.

* 본 방식은 attach.sh\(bat\) 파일을 실행하여 적용하며, 실행 파라미터로 PID\(프로세스 ID\)를 사용합니다.
* 최초 실행 시 attach.sh\(bat\)를 실행하는 과정을 제외하고 설치/실행/업데이트/종료 절차는 ‘javaagent’ 방식과 동일합니다.

**사전 확인**

Linux 계열의 경우 ps 명령을, Windows 계열의 경우 작업관리자를 통해 실행 중인 애플리케이션의 프로세스ID \(PID\)를 확인합니다.Tomcat 예시\(Linux, Web Application Server 종류별로 상이할 수 있습니다\)

```text
$ ps -ef | grep tomcat | grep -v 'grep'
ec2-user  3058     1  1 06:11 pts/0	00:00:02 /home/ec2-user/jdk1.8.0_111/bin/java -Djava.util.logging.config.file=/home/ec2-user/apache-tomcat-7.0.72/conf/logging.properties -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -Djdk.tls.ephemeralDHKeySize=2048 -Djava.endorsed.dirs=/home/ec2-user/apache-tomcat-7.0.72/endorsed -classpath /home/ec2-user/apache-tomcat-7.0.72/bin/bootstrap.jar:/home/ec2-user/apache-tomcat-7.0.72/bin/tomcat-juli.jar -Dcatalina.base=/home/ec2-user/apache-tomcat-7.0.72 -Dcatalina.home=/home/ec2-user/apache-tomcat-7.0.72 -Djava.io.tmpdir=/home/ec2-user/apache-tomcat-7.0.72/temp org.apache.catalina.startup.Bootstrap start
```

**설치**

“javaagent” 방식의 설치와 동일하게 애플리케이션 서버 JVM 옵션에 -javaagent 설정을 추가합니다.

```text
-javaagent:$WHATAP_HOME/whatap.agent.tracer-#.#.#.jar
```

**실행**

$WHATAP\_HOME 경로 하위에서 사전 확인 과정에서 확인한 PID를 파라미터로 부여하여 attach.sh\(bat\)을 실행합니다. 에이전트 정상 동작 확인 절차는 “javaagent” 방식과 동일합니다.

```text
$ ./attach.sh 3058
JAVA_HOME=/jdk1.8.0_111
_      ____   	______
| | /| / / /  ___ /_  __/__ ____
| |/ |/ / _ \/ _ `// / / _ `/ _ \
|__/|__/_//_/\_,_//_/  \_,_/ .__/
            	         /_/
Just Tap, Always Monitoring
WhaTap Agent version 0.4.2 20161123
Admin: ec2-user
PID: 3128
Java Path: /jdk1.8.0_111/jre
Java Version: 1.8.0_111
AttachAgent Success :  [3058] org.apache.catalina.startup.Bootstrap start
```

**javaagent 방식**

본 방식으로 에이전트를 구동하는 경우 해당 애플리케이션 서버의 재부팅을 필요로 합니다.

**설치**

애플리케이션 서버 JVM 옵션에 -javaagent 설정을 추가합니다.

```text
-javaagent:$WHATAP_HOME/whatap.agent.tracer-#.#.#.jar
-javaagent 프로퍼티 값은 $WHATAP_HOME/whatap.agent.tracer-#.#.#.jar의  절대 경로입니다. 애플리케이션 서버에 따라 별도의 프로퍼티를 추가해야 하는 경우도 있으며, 이는 ‘애플리케이션 서버 별 적용 절차’에서 확인할 수 있습니다.
```

**Tomcat – Linux 계열**

Tomcat의 경우 웹 애플리케이션 서버를 구동하는 파일\(톰캣의 경우 Catalina\)의 상단에 JAVA\_OPTS를 부여합니다.

```text
#   JAVA_OPTS   	(Optional) Java runtime options used when any command
#     	is executed.
#     	Include here and not in CATALINA_OPTS all options, that
#     	should be used by Tomcat and also by the stop process,
#     	the version command etc.
#     	Most options should go into CATALINA_OPTS.
########## WHATAP ############
JAVA_OPTS="${JAVA_OPTS} -javaagent:/whatap/whatap.agent.tracer-0.4.2.jar "
########## WHATAP ############
```

항상 $WHATAP\_HOME 디렉토리에 설치된 최상위 버전의 에이전트로 기동하고자 하는 경우, 아래와 같은 스크립트를 적용해줍니다.

```text
WHATAP_HOME=/whatap
########## WHATAP ############
WHATAP_JAR=`ls ${WHATAP_HOME}/whatap.agent.tracer-*.jar | sort | tail -1`
JAVA_OPTS="${JAVA_OPTS} -javaagent:${WHATAP_JAR} "
########## WHATAP ############
```

**Tomcat – Windows 계열**

```text
rem   JAVA_OPTS   	(Optional) Java runtime options used when any command
rem     	is executed.
rem     	Include here and not in CATALINA_OPTS all options, that
rem     	should be used by Tomcat and also by the stop process,
rem     	the version command etc.
rem     	Most options should go into CATALINA_OPTS.
rem ########## WHATAP ############
if x%JAVA_OPTS:whatap=%==x%JAVA_OPTS% (
  set JAVA_OPTS=%JAVA_OPTS% -javaagent:C:\whatap\whatap.agent.tracer-0.4.2.jar
)
rem ########## WHATAP ############
```

항상 $WHATAP\_HOME 디렉토리에 설치된 최상위 버전의 에이전트로 기동하고자 하는 경우, 아래와 같은 스크립트를 적용해줍니다.

```text
rem ########## WHATAP ############
set WHATAP_HOME=C:\whatap
for /f %%f in ('dir /b /on %WHATAP_HOME%\whatap.agent.tracer-*.jar') do set last=%%f
set WHATAP_JAR=%last%
if x%JAVA_OPTS:whatap=%==x%JAVA_OPTS% (
  set JAVA_OPTS=%JAVA_OPTS% -javaagent:%WHATAP_HOME%\%WHATAP_JAR%
)
rem ########## WHATAP ############
```

**실행**

애플리케이션 서버를 기동 또는 재기동 하고, 애플리케이션 서버 로그 및 에이전트 로그를 확인하여 에이전트의 정상 기동 여부를 확인합니다.

```text
Nov 16, 2016 3:06:40 AM org.apache.catalina.startup.HostConfig deployDirectory
INFO: Deployment of web application directory /var/lib/tomcat7/webapps/ROOT has finished in 577 ms
Nov 16, 2016 3:06:40 AM org.apache.coyote.AbstractProtocol start
INFO: Starting ProtocolHandler ["http-bio-8080"]
Nov 16, 2016 3:06:40 AM org.apache.catalina.startup.Catalina start
INFO: Server startup in 3984 ms
_  	 ____       ______
| | /| / / /  ___ /_  __/__ ____
| |/ |/ / _ \/ _ `// / / _ `/ _ \
|__/|__/_//_/\_,_//_/  \_,_/ .__/
        	             /_/
Just Tap, Always Monitoring
WhaTap Agent version 0.3.9 20161115
```

서버에서 정상적으로 로그가 올라온 것을 확인한 뒤, 콘솔에 정상적으로 등록되어 있는 여부를 확인하기 위해 해당 프로젝트의 ‘서버’ 메뉴에 올라온 해당 애플리케이션 서버의 명칭을 확인합니다.[![260](https://github.com/jinronara/deleteme_2/raw/master/images/260.png)](https://github.com/jinronara/deleteme_2/blob/master/images/260.png)

* 애플리케이션명은 {type}-{ip2}-{ip3}-{port\] 의 형태의 식별ID가 부여됩니다. 마지막 요소가 {port}가 아닌 {pid}인 경우 애플리케이션 서버의 서비스 포트가 인식되지 않은 것으로 애플리케이션의 마지막 항목에 표시되는 PID\(프로세스 ID\)를 참조하여 설치 문제에 대응합니다.

**업데이트**

에이전트 설치 파일을 다운로드 받아 압축을 풀고, whatap.agent.tracer-..\#.jar 파일을 $WHATAP\_HOME폴더에 복사합니다.

애플리케이션 서버의 JVM 옵션의 -javaagent 설정을 새로 설치된 whatap.agent.tracer-..\#.jar로 수정하고, 애플리케이션 서버를 재기동 합니다.

* 애플리케이션 서버 재기동 시 항상 최상위 버전으로 적용하고자 하는 경우 위 ‘설치’ 섹션에서 제시된 스크립트를 참조하여 적용하면 됩니다.
* 구 버전의 whatap.agent.tracer-..\#.jar 파일을 삭제하고자 하는 경우, 애플리케이션 서버 재기동 이후에 삭제하도록 합니다.

**중지**

애플리케이션 서버 JVM 옵션의 -javaagent 설정을 삭제하고, 애플리케이션 서버를 재기동 합니다.

* 에이전트 삭제를 희망하는 경우, 애플리케이션 서버 재기동 이후에 삭제하도록 합니다.

#### 로그 \(준비 중\) {#user-content-로그-준비-중}

**로그파일 종류**

**정상 동작 확인**

#### 애플리케이션 서버 별 적용절차 {#user-content-애플리케이션-서버-별-적용절차}

**애플리케이션 서버 별 JVM 옵션 설정 위치**

| 애플리케이션 서버 | 설정 위치 |
| :--- | :--- |
| SpringBoot | java -javaagent:{whatap.agent.tracer-x.x.x.jar의 full path} -jar {application jar} |
| Tomcat | $CATALINA\_HOME/bin/catalina.sh\(bat\) |
| JBoss 5.0 이하 | $JBOSS\_HOME/bin/run.conf |
| JBoss 7.0 이상 EAP 6.0이상 | $JBOSS\_HOME/bin/standalone.conf\(domain.conf\) |
| WebLogic | $WEBLOGIC\_HOME/user\_projects/domains/사용자도메인/bin/startWebLogic.sh\(bat\) |
| WebSphere | admin console 통해 1. Server &gt; Server Types &gt; WebSphere application servers &gt; 서버 선택 2. 서버 Configuration탭 &gt; Server Infrastructure의 Java and Process Management &gt; Process definition 선택 3. Additional Properties의 Java Virtual Machine 선택 4. Generic JVM arguments 편집 |
| Jeus7 | $JEUS\_HOME/domains/jeus\_domain/config.xml |
| Jeus6 | $JEUS\_HOME/config/$hostname/JEUSMain.xml |
| Jetty | watch\_jetty.sh\(bat\) |

**SpringBoot**

jar 형태로 패키징하여 실행하는 경우 jvm 옵션에 -javaagent를 추가합니다.

```text
java -javaagent:{whatap.agent.tracer-x.x.x.jar의 full path} -jar {application jar}
```

**Tomcat on Windows Service**

Windows 계열 OS에 binary로 설치하여 SYSTEM 계정으로 실행한 경우, ‘javaagent’ 방식으로 Tomcat을 실행합니다.

* “Configure Tomcat” 프로그램을 실행하여 Java 탭 선택 &gt; Java Options에 -javaagent 옵션을 지정합니다.

[![270](https://github.com/jinronara/deleteme_2/raw/master/images/270.png)](https://github.com/jinronara/deleteme_2/blob/master/images/270.png)

**JBoss**

**javaagent + onetime attach 방식**

1. javaagent 방식과 동일하게 JVM 옵션을 추가합니다.

standalone.sh 설정 추가 예

```text
#!/bin/sh
########## WHATAP ############
WHATAP_HOME=/home/ec2-user/whatap
WHATAP_JAR=`ls ${WHATAP_HOME}/whatap.agent.tracer-*.jar | sort | tail -1`
JAVA_OPTS="${JAVA_OPTS} -javaagent:${WHATAP_JAR} -Djboss.modules.system.pkgs=whatap "
########## WHATAP ############
```

1. JBOSS의 PID\(프로세스 ID\)를 확인합니다.

```text
$ ps -ef | grep jboss | grep -v 'grep'
ec2-user 27757 27714 13 12:21 pts/2    00:00:03 /jdk1.7.0_79/bin/java -D[Standalone] -server -XX:+UseCompressedOops -XX:+TieredCompilation -Djboss.modules.system.pkgs=whatap -Dorg.jboss.boot.log.file=/jboss-as-7.1.1.Final/standalone/log/boot.log -Dlogging.configuration=file:/jboss-as-7.1.1.Final/standalone/configuration/logging.properties -jar /jboss-as-7.1.1.Final/jboss-modules.jar -mp /jboss-as-7.1.1.Final/modules -jaxpmodule javax.xml.jaxp-provider org.jboss.as.standalone -Djboss.home.dir=/jboss-as-7.1.1.Final
```

1. attach.sh 스크립트를 실행합니다.

```text
$ ./attach.sh 27757
JAVA_HOME=/jdk1.7.0_79
_      ____       ______
| | /| / / /  ___ /_  __/__ ____
| |/ |/ / _ \/ _ `// / / _ `/ _ \
|__/|__/_//_/\_,_//_/  \_,_/ .__/
                         /_/
Just Tap, Always Monitoring
WhaTap Agent version 0.4.5 20161207
Admin: ec2-user
PID: 27848
Java Path: /jdk1.7.0_79/jre
Java Version: 1.7.0_79
AttachAgent Success :  [27757] /jboss-as-7.1.1.Final/jboss-modules.jar -mp /jboss-as-7.1.1.Final/modules -jaxpmodule javax.xml.jaxp-provider org.jboss.as.standalone -Djboss.home.dir=/jboss-as-7.1.1.Final
```

**javaagent 방식**

JVM 옵션에 -javaagent 및 -Djboss.modules.system.pkgs에 설정을 추가합니다.

| 애플리케이션 서버 버전 | JVM 옵션 |
| :--- | :--- |
| 공통 | JVM 옵션의 -javaagent에 Tracer 설정 |
| JBOSS 7.0 이상 EAP 6.0이상 | JVM 옵션의 -Djboss.modules.system.pkgs 환경 변수에 “whatap” prefix 추가 |

standalone.sh 설정 추가 예

```text
#!/bin/sh
########## WHATAP ############
WHATAP_HOME=/home/ec2-user/whatap
WHATAP_JAR=`ls ${WHATAP_HOME}/whatap.agent.tracer-*.jar | sort | tail -1`
JAVA_OPTS="${JAVA_OPTS} -javaagent:${WHATAP_JAR} -Djboss.modules.system.pkgs=whatap "
########## WHATAP ############
```

“-Djboss.modules.system.pkgs=whatap” 미설정 시 에러 메세지

```text
11:38:46,148 ERROR [org.apache.catalina.core.ContainerBase.[jboss.web].[default-host].[/].[default]] (http--0.0.0.0-8080-1) Servlet.service() for servlet default threw exception: java.lang.ClassNotFoundException: whatap.agent.trace.TraceMain from [Module "javax.servlet.api:main" from local module loader @67d7d474 (roots: /jboss-as-7.1.1.Final/modules)]
```

**WebLogic**

javaagnet 방식 적용 시의 설정 예시를 제시합니다.설정 위치

$WEBLOGIC\_HOME/user\_projects/domains/사용자도메인/bin/startWebLogic.sh\(bat\)

* javaagent 프로퍼티 설정을 추가합니다.
  * $WEBLOGIC\_HOME은 WebLogic 설치 경로를 가리킵니다.

[![280](https://github.com/jinronara/deleteme_2/raw/master/images/280.png)](https://github.com/jinronara/deleteme_2/blob/master/images/280.png)Figure 1. 예시

**WebSphere**

에이전트 방식만 지원하며, Web Console을 통한 설정 방법을 제시합니다.

1. 먼저 웹브라우저를 통해 admin console에 로그인 합니다.

[![290](https://github.com/jinronara/deleteme_2/raw/master/images/290.png)](https://github.com/jinronara/deleteme_2/blob/master/images/290.png)

1. Servers &gt; Server Type &gt; WebSphere application servers 메뉴를 통해 에이전트를 설치할 서버를 선택합니다.

[![300](https://github.com/jinronara/deleteme_2/raw/master/images/300.png)](https://github.com/jinronara/deleteme_2/blob/master/images/300.png)

1. 선택된 서버 Configuration 탭에 Server Infrastructure의 Java and Process Management &gt; Process definition 메뉴를 선택합니다.

[![310](https://github.com/jinronara/deleteme_2/raw/master/images/310.png)](https://github.com/jinronara/deleteme_2/blob/master/images/310.png)

1. Additional Properties의 Java Virtual Machine 메뉴를 선택합니다.

[![320](https://github.com/jinronara/deleteme_2/raw/master/images/320.png)](https://github.com/jinronara/deleteme_2/blob/master/images/320.png)

1. WEBSHERE의 서비스 포트를 확인합니다.

[![330](https://github.com/jinronara/deleteme_2/raw/master/images/330.png)](https://github.com/jinronara/deleteme_2/blob/master/images/330.png)

1. Configuration 탭의 Generic JVM arguments에 -javaagent와 -Dwhatap.port를 추가합니다.

[![340](https://github.com/jinronara/deleteme_2/raw/master/images/340.png)](https://github.com/jinronara/deleteme_2/blob/master/images/340.png)리눅스 계열

-javaagent:/home/wasadmin/whatap/whatap.agent.tracer-\#.\#.\#.jar -Dwhatap.port=9443윈도우 계열

-javaagent:C:\whatap\whatap.agent.tracer-\#.\#.\#.jar -Dwhatap.port=9443

**Jeus**

‘javaagent’ 방식을 적용하는 경우, 다음 절차를 통해 설치합니다.

1. Jeus 설정 파일에서 JVM 옵션을 설정합니다

|  | 설정 파일 위치 |
| :--- | :--- |
| Jeus7 | $JEUS\_HOME/domains/jeus\_domain/config.xml 에서 jvm-option에 -javaagent 옵션을 추가합니다. |
| Jeus6 | $JEUS\_HOME/config/$hostname/JEUSMain.xml 에서 command-option에 -javaagent 옵션을 추가합니다. |

* $JEUS\_HOME은 JEUS 설치 경로를 가리킵니다.

Jeus 7 예시

```text
<domain>
   <servers>
       <server>
           <name>server1</name>
           <jvm-config>
               <jvm-option>
                   -Xmx1024m -XX:MaxPermSize=128m
                   -javaagent:/whatap/whatap.agent.tracer-0.8.1.jar
               </jvm-option>
           </jvm-config>
       </server>
   </servers>
</domain>
```

[![350](https://github.com/jinronara/deleteme_2/raw/master/images/350.png)](https://github.com/jinronara/deleteme_2/blob/master/images/350.png)Figure 2. Jeus 6 예시

1. 애플리케이션 서버를 재기동 시킵니다.

[![360](https://github.com/jinronara/deleteme_2/raw/master/images/360.png)](https://github.com/jinronara/deleteme_2/blob/master/images/360.png)

1. 애플리케이션 서버 로그와 에이전트 로그를 통해 에이전트가 정상적으로 기동하였는지, 에러가 발생하지 않았는지 확인합니다.

|  | 로그 파일 위치 |
| :--- | :--- |
| 에이전트 | $WHATAP\_HOME/logs/whatap-{SERVER\_NAME}-{DATE}.log |
| JEUS6 | $JEUS\_HOME/logs/$NODE\_NAME/JeusServer.log |
| JEUS7 | $JEUS\_HOME/domains/$HOST\_NAME/servers/$NODE\_NAME/logs/JeusServer.log |

JEUS7 예시

\($JEUS\_HOME/domains/$HOST\_NAME/servers/$NODE\_NAME/logs/JeusServer.log\)[![370](https://github.com/jinronara/deleteme_2/raw/master/images/370.png)](https://github.com/jinronara/deleteme_2/blob/master/images/370.png)

1. 에이전트가 애플리케이션 서버의 종류와 애플리케이션 서버의 서비스 container명을 인식했는지 확인합니다.

와탭 사이트에서 whatap.name과 whatap.type을 확인합니다. whatap.io 사이트에 로그인 &gt; “APM” 제품 선택 &gt; 프로젝트의 Application Servers 메뉴 선택 &gt; 설치한 JEUS 서버 &gt; Boot Environment 메뉴 선택을 통해 확인합니다.

whatap.type에는 애플리케이션 서버의 종류가 명시되어야 하며, whatap.name의 마지막 요소가 container이름 이어야 합니다.[![380](https://github.com/jinronara/deleteme_2/raw/master/images/380.png)](https://github.com/jinronara/deleteme_2/blob/master/images/380.png)

**Jetty**

JVM 옵션에 -javaagent와 -Dwhatap.port를 추가합니다.

Jetty 실행 스크립트

* $JETTY\_HOME/bin/jetty.sh 파일에 JVM 파일 옵션을 추가합니다.
  * 이후 본 문서에서 $JETTY\_HOME은 Jetty 설치 경로를 가리킵니다.

[![390](https://github.com/jinronara/deleteme_2/raw/master/images/390.png)](https://github.com/jinronara/deleteme_2/blob/master/images/390.png)

* java 실행 옵션에 설정
  * $JETTY\_HOME/bin 경로로 이동 후, 하기 옵션을 적용하여 Jetty를 기동합니다.

```text
$ java -javaagent:/home/vagrant/whatap/whatap.agent.tracer-0.3.0.jar -Dwhatap.port=8080 -jar start.jar &
```

**Resin**

‘javaagent’ 방식을 적용하는 경우, 다음 절차를 통해 설치합니다.

1. Resin 설정 파일에서 JVM 옵션을 설정합니다.

|  | 설정 파일 위치 |
| :--- | :--- |
| Resin 4.x | $RESIN\_HOME/conf/resin.properties 에서 jvm-arg를 추가하여 -javaagent 옵션을 설정합니다. |

Resin4.x 예시

```text
(중략)
<resin xmlns="http://caucho.com/ns/resin">
   <cluster id="web-tier">
       <server-default>
           <jvm-arg>-Xmx1024m -XX:MaxPermSize=128m -javaagent:/whatap/whatap.agent.tracer-#.#.#.jar</jvm-arg>
       </server-default>
       ...
   </cluster>
</resin>
(중략)
```

1. 애플리케이션 서버를 재기동 시킵니다.
2. 애플리케이션 서버 로그와 에이전트 로그를 통해 에이전트가 정상적으로 기동 되었는지 에러가 발생하지 않았는지 확인합니다.

|  | 로그 파일 위치 |
| :--- | :--- |
| 에이전트 | $WHATAP\_HOME/logs/whatap-{SERVER\_NAME}-{DATE}.log |
| RESIN4.x | $RESIN\_HOME/log/jvm-app-\#.log |

#### 설치 에러 대응 {#user-content-설치-에러-대응}

**방화벽 설정 확인**

와탭 서버에 대한 TCP 아웃바운드 방화벽이 설정되어 있으면 모니터링 정보를 서버로 전송 할 수 없으므로 방화벽 차단을 해제해야 합니다.

**방화벽 확인 방법 \(telnet 서버IP 서버포트\)**

telnet 명령 수행 시 하기와 같은 접속 관련 정보가 표시되어야 정상입니다.

```text
$ telnet 52.193.60.176 6600
Trying 52.193.60.176...
Connected to 52.193.60.176.
Escape character is '^]'.
```

* 수집 서버 정보는 와탭 웹사이트에서 해당 프로젝트의 관리 &gt; 에이전트 설치 메뉴에서 확인할 수 있습니다.

**애플리케이션 서비스 포트가 감지되지 않는 경우**

모니터링 대상은 인식하였으나 서비스 포트를 감지하지 못하는 경우, 에이전트는 와탭 서버로 포트 대신 PID\(프로세스 ID\)를 전송합니다. 이는 와탭 사이트의 모니터링 대상 서버 목록을 통해 포트가 감지되지 않은 서버를 PID로 식별하여 조치 할 수 있도록 하기 위함입니다. 서비스 포트 감지에 실패한 애플리케이션 서버 확인을 위하여 와탭 사이트의 하기 경로를 통해 애플리케이션 서버 정보를 확인합니다.

* 해당 프로젝트의 서버 메뉴 &gt; 해당 서버의 More 버튼 &gt; Boot Environment 선택

[![400](https://github.com/jinronara/deleteme_2/raw/master/images/400.png)](https://github.com/jinronara/deleteme_2/blob/master/images/400.png)Figure 3. Tomcat 예시

이런 경우 아래와 같이 애플리케이션 서버 실행스크립트에 명시된 JVM 옵션에 whatap.port 시스템 프로퍼티를 추가한 후 애플리케이션 서버를 재기동합니다.

```text
JAVA_OPTS="${JAVA_OPTS} -Dwhatap.port=8080 "
```

* 애플리케이션 서버 별 JVM 옵션 설정 파일은 ‘애플리케이션 서버 별 적용절차’에서 확인할 수 있습니다.

**애플리케이션 서버가 OSGi 프레임워크를 사용하는 경우**

7.0 이상 버전의 JBOSS AP, 6.x 버전 이상의 JBOSS EAP, WebSphere 같이 OSGI 프레임워크 구조의 애플리케이션 서버 실행 파일의 JVM 옵션에 에이전트 패키지 prefix\(whatap\)을 등록합니다.

* OSGI애플리케이션에서 에이전트 클래스 참조를 위해 추가하는 설정입니다.

**JBoss AS 7.0이상, JBoss EAP 6.0 이상**

$JBOSS\_HOME/bin/standalone.conf\(domain.conf\)파일에 prefix를 등록합니다.[![410](https://github.com/jinronara/deleteme_2/raw/master/images/410.png)](https://github.com/jinronara/deleteme_2/blob/master/images/410.png)Figure 4. JBOSS .EAP 7.0 예시

**WebSphere**

Default로 서브 컨테이너 라이브러리의 상호 참조가 허용되어 있는 경우 별도의 설정이 필요하지 않습니다. 서브 컨테이너 라이브러리의 상호 참조가 허용되지 않는 오류가 발생하는 경우, 와탭 패키지 자체가 로딩 되지 않으므로, 하기 설정을 JVM Option에 추가합니다.

* -Dcom.ibm.ws.classloader.server.alwaysAllowedPackages=whatap
  * Default로 ‘\*’로 지정되어 있는 경우는 별도의 설정을 필요로 하지 않습니다.
  * 설정 위치는 ‘WebSphere‘를 참조합니다.

필요에 따라 하기의 설정을 적용합니다. \(java 프로세스를 먼저 확인하여 -Dorg.osgi.framework.bootdelegation가 \*로 지정된 경우는 설정 하지 않습니다.\)

OSGi 컨테이너로 Eclipse Equinox를 활용하므로, 와탭 패키지를 OSGi bootdelegation 시스템 프로퍼티에 추가합니다.

* -Dorg.osgi.framework.bootdelegation=…​,whatap.\*
  * Default로 ‘\*’로 지정되어 있는 경우는 별도의 설정을 필요로 하지 않습니다.
  * 설정 위치는 ‘WebSphere’를 참조합니다.

**security.policy 권한 추가**

$WEBSPHERE\_HOME/properties/server.policy 또는 $WEBSPHERE\_PROFILE\_HOME/properties/server.policy 파일에 아래와 같이 권한을 추가합니다.

```text
grant codeBase "file:$WHATAP_HOME/-"
{
   permission java.security.AllPermission;
};
```

**히트맵에 트랜잭션이 표시되지 않는 경우**

**IBM JDK**

IBM JDK의 경우 “watcher” 방식으로 에이전트를 실행시킬 경우 트랜잭션 정보가 수집되지 않으므로 ‘javaagent’ 방식으로 에이전트를 실행해야 합니다.

**logmanager 관련 에러가 발생하는 경우**

**JBoss AS 7.0이상, JBoss EAP 6.0 이상**

$WHATAP\_HOME/logs/whatap-{SERVER\_NAME}-{DATE}.log 파일의 whatap.error에 해당 에러가 출력된 경우 하기 JVM 옵션을 설정합니다.

* -Djava.util.logging.manager에 LogManager package명 설정
* -Xbootclassloader에 JBoss log manager JAR file 설정

[![420](https://github.com/jinronara/deleteme_2/raw/master/images/420.png)](https://github.com/jinronara/deleteme_2/blob/master/images/420.png)Figure 5. 설정 추가 예

**MBeanServerBuilder 에러가 발생하는 경우**

**JBoss 5.0 이하**

$WHATAP\_HOME/logs/whatap-{SERVER\_NAME}-{DATE}.log 파일의 whatap.error에 해당 에러가 출력된 경우 하기 JVM 옵션을 설정합니다.

* -Djboss.platform.mbeanserver를 true로 설정합니다.

[![430](https://github.com/jinronara/deleteme_2/raw/master/images/430.png)](https://github.com/jinronara/deleteme_2/blob/master/images/430.png)Figure 6. 설정 추가 예

**permission 오류가 발생하는 경우**

Java Security Policy 관련 오류가 발생하는 경우, $JAVA\_HOME/jre/lib/security/java.policy 파일에 권한 설정을 추가합니다.

**권한 일괄 허용**

최소한의 권한 설정을 적용하지 않고, 모든 권한을 일괄 적용하고자 하는 경우, {JAVA\_HOME}/jre/lib/security/java.policy 파일에 하기의 설정을 추가합니다.

```text
grant {
   permission java.security.AllPermission;
};
```

**java.io.FilePermission 오류가 발생하는 경우**

[![440](https://github.com/jinronara/deleteme_2/raw/master/images/440.png)](https://github.com/jinronara/deleteme_2/blob/master/images/440.png)

$JAVA\_HOME/jre/lib/security/java.policy 파일에 하기의 설정을 추가합니다.

```text
grant {
   ...
   permission java.io.FilePermission {오류 메세지에서 확인된 패키지 경로}, "read"
};
```

**java.util.PropertyPermission 오류가 발생하는 경우**

$JAVA\_HOME/jre/lib/security/java.policy 파일에 하기의 설정을 추가합니다.

```text
grant {
   ...
   permission java.util.PropertyPermission {오류 메세지에서 확인된 패키지 경로}, "read"
};
```

**Sigar library를 로딩하지 못하는 경우**

$WHATAP\_HOME/lib1/\*.so 파일에 실행 권한이 부여되어 있는지 확인합니다.

미부여 시에는 하기 명령을 통해 실행 권한을 부여합니다.

```text
$ sudo chmod +x *.so
```

[![440](https://github.com/jinronara/deleteme_2/raw/master/images/440.png)](https://github.com/jinronara/deleteme_2/blob/master/images/440.png)

AIX 7에서 $WHATAP\_HOME/lib1 하위에 libsigar-ppc64-aix-7.so 파일이 존재하지 않아 오류가 발생한 경우, sigar-ppc64-aix-5.so 파일을 복제하여 sigar-ppc64-aix-7.so 파일로 복제하여 주시기 바랍니다.

#### FAQ {#user-content-faq}

**서버명을 임의로 부여하여 관리하고 싶은 경우**

에이전트는 애플리케이션 서버 종류와 애플리케이션 서버의 IP, 서비스 포트를 사용하여 자동으로 서버명을 부여합니다.

자동으로 부여된 이름 대신 직접 애플리케이션 서버별로 이름을 부여하고 싶은 경우, 애플리케이션 서버의 JVM 옵션으로 애플리케이션명을 명시적으로 지정할 수 있습니다.

**애플리케이션명 지정 옵션**

| 우선순위 | 옵션 | 설정위치 | 설명 |
| :--- | :--- | :--- | :--- |
| 1 | -Dwhatap.name | JVM Option | 어플리케이션명 패턴을 지정합니다.default : {type}-{ip2}-{ip3}-{port} |
| 2 | -Dwhatap.oname | JVM Option | 어플리케이션명을 고정값으로 지정합니다. |

**애플리케이션명 패턴**

프로젝트에 등록된 애플리케이션 서버별로 동일한 이름이 사용되면 안되므로 서버명을 고정으로 사용해서는 안됩니다. Internal ip address로 인해 서버 ip가 중복되는 경우는 애플리케이션 서버명을 그룹 단위로 패턴화하여 적용할 수 있습니다.

| 패턴 옵션 | 설명 |
| :--- | :--- |
| type | 어플리케이션 서버 유형 |
| ipN | ip address의 N 번째 자리 |
| port | 어플리케이션 서비스 포트 |
| pid | 어플리케이션 프로세스 ID |

**애플리케이션명 옵션 적용 예시**

Jetty 예시

JVM 옵션에 -Dwhatap.name=sale1-192-168-111 를 지정한 예시입니다.[![460](https://github.com/jinronara/deleteme_2/raw/master/images/460.png)](https://github.com/jinronara/deleteme_2/blob/master/images/460.png)Figure 7. 예시

Jetty 및 에이전트 실행 후, 와탭 사이트의 하기 경로에서 등록한 이름으로 서버가 등록된 것을 확인할 수 있습니다.

* whatap.io 사이트에 로그인 &gt; “APM” 제품 선택 &gt; 프로젝트의 Application Servers 메뉴 선택

#### 확장 기능 {#user-content-확장-기능}

**AES 256 암호화 적용**

와탭 APM 에이전트는 수집된 데이터를 암호화하여 서버로 전송합니다. 데이터의 중요도나 설정에 따라 이를 변경할 수 있습니다. 기본적으로 XOR 연산과 AES 알고리즘을 통한 암호화를 사용하며 평문을 128비트 단위로 나누어 암호화, 복호화를 수행하며, 사용자의 설정에 따라 256비트까지 확장할 수 있습니다.

**설치**

기본적으로 JCE는 128비트를 지원하고 있기 때문에 AES 256 비트를 적용하기 위해서는 아래 패치를 통해 256비트까지 확장해서 사용할 수 있게 해야 합니다.

* 기본적인 환경에서 AES 256 적용시 다음과 같은 오류 발생

```text
Unsupported keysize or algorithm parameters.
##혹은,
Illegal key size or default parameters.
```

* Java 7
  * [http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
* Java 6
  * [http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)
* Java 5
  * [http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-java-plat-419418.html\#jce\_policy-1.5.0-oth-JPR](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-java-plat-419418.html#jce_policy-1.5.0-oth-JPR)
* Java 1.42
  * [http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-java-plat-419418.html\#7503-jce-1.4.2-oth-JPR](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-java-plat-419418.html#7503-jce-1.4.2-oth-JPR)

위의 파일을 다운로드 한 후 $JAVA\_HOME/jre/lib/security에 파일을 덮어씁니다.

**설정**

와탭 APM 에이전트가 설치된 디렉토리에서 whatap.conf 파일에 아래와 같은 설정을 추가합니다.cypher\_level=256 설정을 추가합니다.

```text
license=[라이선스 키]
whatap.server.host=52.78.209.94/52.78.224.235
cypher_level=256
```

**재실행**

설정을 추가한 후 WAS를 재기동합니다.

**에이전트 Ping**

모니터링 기능을 적용하기 앞서 Tracer와 서버 간의 통신에 문제가 없는지 확인하기 위한 기능을 제공합니다. 사용자는 ping.sh를 실행하여 에이전트를 통해 가상의 모니터링 정보를 서버로 송신할 수 있으며, whatap.io 사이트에 정보가 정상 송신되는 지의 여부를 확인할 수 있습니다.

**실행**

```text
$ ./ping.sh
JAVA_HOME=/jdk1.8.0_111
 _      ____       ______
| | /| / / /  ___ /_  __/__ ____
| |/ |/ / _ \/ _ `// / / _ `/ _ \
|__/|__/_//_/\_,_//_/  \_,_/ .__/
                          /_/
Just Tap, Always Monitoring
WhaTap Agent version 0.4.5 20161207
20161208 09:02:25.003 SEND PING DATA
20161208 09:02:25.510 SEND PING DATA
(생략)
```

5.3.7.2.2. 확인 에이전트가 설치된 서버와 수집 서버 간의 통신이 정상적으로 수행되었다면 whatap.io 사이트에서 하기와 같은 화면을 확인할 수 있습니다.

* 대시보드

가상의 액티브 트랜잭션 수가 30으로 나타납니다.[![470](https://github.com/jinronara/deleteme_2/raw/master/images/470.png)](https://github.com/jinronara/deleteme_2/blob/master/images/470.png)

* 애플리케이션 서버

서버로 데이터를 송신중인 가상의 에이전트가 NET-PING-{PID}의 애플리케이션 명으로 등록되어 있는 것을 확인할 수 있습니다.[![480](https://github.com/jinronara/deleteme_2/raw/master/images/480.png)](https://github.com/jinronara/deleteme_2/blob/master/images/480.png)

#### 제약 사항 {#user-content-제약-사항}

whatap.io 사이트에서 프로젝트 생성 시, 지역\(Region\)은 중복 선택이 불가하며 복수의 지역\(Region\)을 활용하는 경우 별도의 프로젝트를 생성해야 합니다.

Cloud 환경과 같이 복수의 지역\(Region\)에 서버가 존재하는 경우, 네트워크 latency 등 성능 정보 수집 상의 제약 사항을 회피하기 위하여 지역\(Region\)단위로 수집 서버를 위치시켜야 합니다. 와탭은 고객 요구 사항에 부응하기 위하여 지역\(Region\)별로 수집 서버를 구축합니다.

와탭 APM 모니터링은 에이전트의 식별을 위한 용도로 에이전트의 IP 주소와 Port 정보를 활용하기 때문에 사용자 환경의 모니터링 대상 애플리케이션 서버가 동일 IP, 동일 Port를 사용하는 경우 와탭 서버에서 해당 서버 인스턴스를 구분 할 수 없게 됩니다.

* 서버 인스턴스가 동적으로 확장되는 환경이 아니라면’서버명을 임의로 부여하여 관리하고 싶은 경우’를 참조하여 애플리케이션 식별을 위한 명칭을 직접 지정하는 방식을 통해 우회 할 수 있습니다.
* 와탭에서는 현재 모니터링 대상 애플리케이션이 internal address 또는 네트워크 가상화로 인해 중복된 IP를 사용할 경우,’서버명을 임의로 부여하여 관리하고 싶은 경우’를 참고하여 별도의 애플리케이션명 패턴을 활용합니다.

IBM JDK의 경우 “watcher” 방식으로 에이전트를 실행시킬 경우 트랜잭션 정보가 수집되지 않으므로 “javaagent” 방식만을 지원합니다.

* JVM Optimization을 저해하여 성능 저하를 유발할 가능성으로 인해 코드 주입을 제한하고 있습니다.

#### 호환성 목록 {#user-content-호환성-목록}

**WAS**

Java 버전 별로 다양한 WAS에서 와탭 에이전트 호환성 테스트를 수행한 결과입니다.

**Tomcat**

| WAS Ver. | java se6 \(jdk1.6.0\) | java se7 \(jdk1.7.0\_80\) | java se8 \(jdk1.8.0\_91\) |
| :--- | :--- | :--- | :--- |
| tomcat6 | ok | ok | ok |
| tomcat7 | ok | ok | ok |
| tomcat8 | not ok | ok | ok |
| tomcat9 | not ok | not ok | ok |

| WAS Ver. | open jdk6 \(1.6.0\_45\) | open jdk7 \(1.7.0\_80\) | open jdk8 \(1.8.0\_91\) |
| :--- | :--- | :--- | :--- |
| tomcat6 | ok | ok | ok |
| tomcat7 | ok | ok | ok |
| tomcat8 | not ok | ok | ok |
| tomcat9 | not ok | not ok | ok |

| WAS Ver. | ibm-java-x86\_64-60 | ibm-java-x86\_64-71 | ibm-java-x86\_64-80 |
| :--- | :--- | :--- | :--- |
| tomcat6 | ok | ok | ok |
| tomcat7 | ok | ok | ok |
| tomcat8 | not ok | ok | ok |
| tomcat9 | not ok | not ok | ok |

**Jeus**

| WAS Ver. | java se6 \(jdk1.6.0\) | java se7 \(jdk1.7.0\_80\) | java se8 \(jdk1.8.0\_91\) |
| :--- | :--- | :--- | :--- |
| jeus6 | ok | ok | not ok |
| jeus7 | ok | ok | not ok |

| WAS Ver. | open jdk6 \(1.6.0\_45\) | open jdk7 \(1.7.0\_80\) | open jdk8 \(1.8.0\_91\) |
| :--- | :--- | :--- | :--- |
| jeus6 | ok | ok | not ok |
| jeus7 | ok | ok | not ok |

| WAS Ver. | ibm-java-x86\_64-60 | ibm-java-x86\_64-71 | ibm-java-x86\_64-80 |
| :--- | :--- | :--- | :--- |
| jeus6 | ok | ok | not ok |
| jeus7 |  |  |  |

**WebLogic**

업데이트 예정

**WebSphere**

| WAS Ver. | ibm-java-x86\_64-60 |
| :--- | :--- |
| 8.5.5.10 | ok |

**JBOSS**

JDK 6 이상 버전에서 지원되는 JBOSS Comunity, EAP, Wildfly의 모든 버전을 지원 합니다.

| WAS Ver. | java se6 \(jdk1.6.0\) | java se7 \(jdk1.7.0\_80\) | java se8 \(jdk1.8.0\_91\) |
| :--- | :--- | :--- | :--- |
| jboss EAP 7.0 \(standalone\) | not ok | not ok | ok |
| jboss EAP 6.1.1 \(standalone\) | not ok | ok | not ok |
| jboss EAP 6.2 \(standalone\) | not ok | ok | ok |
| jboss EAP 6.3 \(standalone\) | not ok | ok | ok |
| jboss EAP 6.4 \(standalone\) | not ok | ok | ok |
| jboss EAP 7.0 \(domain\) | not ok | not ok | ok |
| jboss AS 5.1.0 \(default\) | ok | ok | ok |

| WAS Ver. | open jdk6 \(1.6.0\_45\) | open jdk7 \(1.7.0\_80\) | open jdk8 \(1.8.0\_91\) |
| :--- | :--- | :--- | :--- |
| jboss EAP 7.0 \(standalone\) | not ok | not ok | ok |
| jboss EAP 6.1.1 \(standalone\) | not ok | ok | not ok |
| jboss EAP 6.2 \(standalone\) | not ok | ok | ok |
| jboss EAP 6.3 \(standalone\) | not ok | ok | ok |
| jboss EAP 6.4 \(standalone\) | not ok | ok | ok |
| jboss EAP 7.0 \(domain\) | not ok | not ok | ok |
| jboss AS 5.1.0 \(default\) | ok | ok | ok |

| WAS Ver. | ibm-java-x86\_64-60 | ibm-java-x86\_64-71 | ibm-java-x86\_64-80 |
| :--- | :--- | :--- | :--- |
| jboss EAP 7.0 \(standalone\) | not ok | not ok | ok |
| jboss EAP 6.1.1 \(standalone\) | not ok | ok | not ok |
| jboss EAP 6.2 \(standalone\) | not ok | ok | ok |
| jboss EAP 6.3 \(standalone\) | not ok | ok | ok |
| jboss EAP 6.4 \(standalone\) | not ok | ok | ok |
| jboss EAP 7.0 \(domain\) |  |  |  |
| jboss AS 5.1.0 \(default\) | ok | ok | ok |

**Jetty**

| WAS Ver. | java se6 \(jdk1.6.0\) | java se7 \(jdk1.7.0\_80\) | java se8 \(jdk1.8.0\_91\) |
| :--- | :--- | :--- | :--- |
| Jetty 8.1.21 | not ok | ok | ok |
| Jetty 9.2.18 | not ok | ok | ok |
| Jetty 9.3.12 | not ok | not ok | ok |

| WAS Ver. | ibm-java-x86\_64-60 | ibm-java-x86\_64-71 | ibm-java-x86\_64-80 |
| :--- | :--- | :--- | :--- |
| Jetty 8.1.21 | not ok | ok | ok |
| Jetty 9.2.18 | not ok | ok | ok |
| Jetty 9.3.12 | not ok | not ok | ok |

**DB**

와탭 에이전트가 WAS가 제공하는 Connection pool을 사용하는 웹 애플리케이션의 DB 트랜잭션 프로파일링 기능 여부에 대해 검증한 결과입니다.

**Tomcat**

| DB | JDBC Driver 화일명 | JDBC Ver. | JDK Ver. | 호환성 |
| :--- | :--- | :--- | :--- | :--- |
| Mysql | mysql-connector-java-5.1.39-bin.jar | 5.1.39 | JDK 1.7.0\_80 | ok |
| MariaDB | mariadb-java-client-1.4.6.jar | 1.4.6 | JDK 1.7.0\_80 | ok |
| PostgreSQL | postgresql-9.4.1209.jre7.jar | 9.4.1209 | JDK 1.7.0\_80 | ok |
| AWS aurora | mysql-connector-java-5.1.39-bin.jar | 5.1.39 | JDK 1.7.0\_80 | ok |
| Oracle | ojdbc6-11.2.0.2.0.jar | 11.2.0.2.0 | JDK 1.7.0\_80 | ok |
| DB2 | db2jcc.jar, db2jcc\_license\_cu.jar | 1.4.2 | JDK 1.7.0\_80 | ok |

**Jeus**

| DB | JDBC Driver 화일명 | JDBC Ver. | JDK Ver. | 호환성 |
| :--- | :--- | :--- | :--- | :--- |
| Mysql | mysql-connector-java-5.1.39-bin.jar | 5.1.39 | JDK 1.7.0\_80 | ok |
| MariaDB | mariadb-java-client-1.4.6.jar | 1.4.6 | JDK 1.7.0\_80 | ok |
| PostgreSQL | postgresql-9.4.1209.jre7.jar | 9.4.1209 | JDK 1.7.0\_80 | ok |
| AWS aurora | mysql-connector-java-5.1.39-bin.jar | 5.1.39 | JDK 1.7.0\_80 | ok |
| Oracle | ojdbc6-11.2.0.2.0.jar | 11.2.0.2.0 | JDK 1.7.0\_80 | ok |
| DB2 | db2jcc.jar, db2jcc\_license\_cu.jar | 1.4.2 | JDK 1.7.0\_80 | ok |

**WebLogic**

| DB | JDK Ver. | 호환성 |
| :--- | :--- | :--- |
| Mysql | JDK 1.8.0\_91 | ok |

**WebSphere**

| DB | JDBC Driver 화일명 | JDBC Ver. | JDK Ver. | 호환성 |
| :--- | :--- | :--- | :--- | :--- |
| Mysql | mysql-connector-java-5.1.39-bin.jar | 5.1.39 | JDK 1.7.0\_80 | ok |
| Oracle | ojdbc6-11.2.0.2.0.jar | 11.2.0.2.0 | JDK 1.7.0\_80 | ok |

**JBoss**

| DB | JDBC Driver 화일명 | JDBC Ver. | JDK Ver. | 호환성 |
| :--- | :--- | :--- | :--- | :--- |
| Mysql | mysql-connector-java-5.1.39-bin.jar | 5.1.39 | JDK 1.7.0\_80 | ok |
| MariaDB | mariadb-java-client-1.4.6.jar | 1.4.6 | JDK 1.7.0\_80 | ok |
| PostgreSQL | postgresql-9.4.1209.jre7.jar | 9.4.1209 | JDK 1.7.0\_80 | ok |
| AWS aurora | mysql-connector-java-5.1.39-bin.jar | 5.1.39 | JDK 1.7.0\_80 | ok |
| Oracle | ojdbc6-11.2.0.2.0.jar | 11.2.0.2.0 | JDK 1.7.0\_80 | ok |
| DB2 | db2jcc.jar, db2jcc\_license\_cu.jar | 1.4.2 | JDK 1.7.0\_80 | ok |

**Jetty**

| DB | JDBC Driver 화일명 | JDBC Ver. | JDK Ver. | 호환성 |
| :--- | :--- | :--- | :--- | :--- |
| Mysql | mysql-connector-java-5.1.39-bin.jar | 5.1.39 | JDK 1.7.0\_80 | ok |
| Oracle | ojdbc6-11.2.0.2.0.jar | 11.2.0.2.0 | JDK 1.7.0\_80 | ok |

### Node.JS 애플리케이션 모니터링 \(준비 중\) {#user-content-node-js-애플리케이션-모니터링-준비-중}

#### 에이전트 실행 및 모니터링 개요 {#user-content-에이전트-실행-및-모니터링-개요}

**에이전트 설치 방식 개요**

**구성 파일**

#### 에이전트 설치/실행/업데이트/중지 {#user-content-에이전트-설치-실행-업데이트-중지-1}

**설치**

**프로젝트 생성**

**라이선스 발급**

**실행**

**업데이트**

**중지**

#### 설치 에러 대응 {#user-content-설치-에러-대응-1}

#### FAQ {#user-content-faq-1}

#### 제약 사항 {#user-content-제약-사항-1}

### PHP 애플리케이션 모니터링 {#user-content-php-애플리케이션-모니터링}

#### 에이전트 실행 및 모니터링 개요 {#user-content-에이전트-실행-및-모니터링-개요-1}

와탭 PHP 애플리케이션 모니터링은 PHP 기반 웹 애플리케이션 서버 모니터링 서비스를 제공합니다.

**에이전트 설치 방식 개요**

PHP 모니터링 서비스를 사용하기 위해서는 모니터링 대상 애플리케이션에 모니터링 에이전트를 설치해야 합니다. 설치 방식은 리눅스 패키지 설치로 가능합니다.

* 와탭 저장소\(Repository\)를 설치합니다.
* whatap-php 리눅스 패키지를\(yum, apt-get\) 설치합니다.
* 설정 스크립트를 실행합니다.
* Apache 또는 PHP-FRPM을 재시작 합니다.

설정 스크립트를 통해서 트레이서는 PHP 확장 모듈\(PHP Extension module\)로 등록되고, 에이전트는 whatap-php 서비스\(Service\)로 실행됩니다.[![490](https://github.com/jinronara/deleteme_2/raw/master/images/490.png)](https://github.com/jinronara/deleteme_2/blob/master/images/490.png)

**구성 파일**

모니터링 정보를 수집하기 위한 트레이서, 수집된 정보를 서버에 전송하기 위한 에이전트, 트레이서와 에이전트를 서버에 동적으로 적용하기 위한 설치 스크립트 파일로 구성됩니다.

PHP 모니터링 서비스를 구성하는 각 파일의 역할은 다음과 같습니다.

| 파일명 | 설명 |
| :--- | :--- |
| whatap\_\#\_\#.so | 트레이서 PHP 확장 모듈\(PHP Extension module\)로 추가 되어 정보를 수집하고 수집된 정보를 에이전트로 전송하는 라이브러리입니다. |
| whatap-php\(whatap\_php\) | 에이전트, 트레이서에서 UDP로 전달된 정보를 수집서버로 전송하는 프로그램입니다. |
| /etc/init.d/whatap-php | 서비스 스크립트 |
| whatap\_php | 서비스 실행파일 |
| whatap.ini | 애플리케이션 서버의 데이터를 수집하는 PHP 확장 모듈\(PHP Extension module\)의 설정 정보, 수집서버의 주소와 서버의 프로젝트 라이선스 키가 입력되는 파일입니다. |
| whatap-install-\#.log | 설치 과정에 대한 로그 파일입니다. \(/usr/whata/php/logs\) |
| whatap-boot-\#.log | 에이전트 로그 파일 입니다. \(/usr/whata/php/logs\) |
| install.sh | 웹 애플리케이션 서버에 트레이서를 적용하기 위한 쉘 스크립트입니다. |
| Whatap.php \(sample.php\) | PHP 소스코드에서 사용할 API 레퍼런스 클래스 \(/usr/whatap/php/lib/Whatap.php\) 및 예제 소스 파일\(sample.php\) 입니다. |

**에이전트 이름 식별**

와탭은 모니터링 정보 수집 대상인 애플리케이션 서버 식별을 위한 정보로 기본적으로 애플리케이션 서버로부터 수집한 정보를 활용합니다. 기본적으로 활용하는 정보는 애플리케이션 서버 종류, 애플리케이션 서버의 IP, 서비스 포트를 조합하여 애플리케이션 서버를 고유 식별자로 사용하게 되며 필요에 따라 사용자가 지정한 명칭을 사용하거나 패턴을 변경하여 사용하는 것도 가능합니다. 이때에는 꼭 고유한 값이어야 합니다.

애플리케이션 서버로부터 추출한 정보를 활용하는 이유는 애플리케이션 서버 정지, 네트워크 단절 또는 에이전트 문제로 인한 수집 서버와 에이전트의 통신 단절 상태가 복구되었을 경우, 재 접속된 에이전트로부터 송신되는 정보가 기존 에이전트로부터 송신된 정보와의 연속성을 유지하기 위해서 입니다. 와탭이 애플리케이션 서버를 식별하기 위해 사용하는 기본 패턴은 다음과 같습니다.

* default: {type}-{ip2}-{ip3}-{process}

기본 패턴에 대한 변경은 whatap.ini에서 설정에서 가능합니다.

object\_name default: {type}-{ip2}-{ip3}-{process}

| 설정 | 설명 |
| :--- | :--- |
| Type | app\_name |
| Ip\# | Ip를 .으로 나누었을 때 \#번째 자리\(0부터\) |
| Process | app\_process\_name |
| hostname | 호스트 명 |

#### 에이전트 설치/실행/업데이트/중지 {#user-content-에이전트-설치-실행-업데이트-중지-2}

**공통**

**프로젝트 생성**

서버를 등록하기 위해 우선 프로젝트를 생성합니다. 추가 버튼을 선택하면 아래와 같이 프로젝트 생성 창이 나타납니다. PHP 아이콘을 선택한 뒤, 희망하는 프로젝트명과 데이터 서버 지역\(Region\), 소속하게 될 그룹을 선택한 뒤 프로젝트를 생성합니다.[![500](https://github.com/jinronara/deleteme_2/raw/master/images/500.png)](https://github.com/jinronara/deleteme_2/blob/master/images/500.png)

이후, 생성된 프로젝트를 클릭하여 관리 화면에 진입합니다.[![510](https://github.com/jinronara/deleteme_2/raw/master/images/510.png)](https://github.com/jinronara/deleteme_2/blob/master/images/510.png)

**라이선스 발급**

[![520](https://github.com/jinronara/deleteme_2/raw/master/images/520.png)](https://github.com/jinronara/deleteme_2/blob/master/images/520.png)

프로젝트 관리화면에서는 우선적으로 라이선스를 발급 받습니다. 라이선스 키는 프로젝트별로 귀속되기 때문에, 유출되거나 배포되어서는 안됩니다. 반드시 본인 프로젝트에 서버를 등록할 때에만 이용하시기 바랍니다.

**에이전트 설치**

**패키지 설치**

**RedHat/CentOS**

* 패키지 저장소\(Repository\) 등록

와탭 저장소\(Repository\)를 등록합니다.

```text
$ sudo rpm -Uvh http://repo.whatap.io/centos/5/noarch/whatap-repo-1.0-1.noarch.rpm
```

* 패키지 설치

아래 명령어를 통해 패키지를 설치합니다.

```text
$ sudo yum install whatap-php
```

* PHP 확장 모듈\(PHP Extension module\) 및 whatap-php서비스\(Service\) 등록 PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\)를 자동으로 설치할 경우에 아래와 같이 적용합니다

```text
$ sudo /usr/whatap/php/install.sh
Input license key
xxxxxxxxxxxxxxxx                          # 발급된 라이선스 key 입력

Input whatap.server.host
192.x.x.x                                  # 발급된 서버 IP 입력
```

PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\)를 자동으로 인식하지 못하는 경우 아래와 같이 선택 설치를 진행해야 합니다. 주로 Apache 명령어\(apachectl, httpd, apache2\) 및 PHP 명령어\(CLI\)가 기본 경로\($PATH\)에 설정 되어 있지 않거나, 여러 개의 PHP가 설치되어 PHP 명령어\(CLI\)가 여러 개일 경우에 \(php5, php70, php-zts, zts-php…\) 실제로 적용하고 있는 버전을 선택하여 진행합니다.

```text
$ sudo /usr/whatap/php/install.sh manual

Input license key
xxxxxxxxxxxxxxxx                            # 발급된 라이선스 key 입력

Input whatap.server.host
192.x.x.x                                    # 발급된 서버 IP 입력

Input : which apache or php-fpm ex)/usr/sbin/httpd, /usr/sbin/apache2, /usr/sbin/php-fpm ...
/usr/sbin/httpd                             # apache 및 php-fpm 명령어 위치 입력

Input : which php ex) /usr/bin/php, /usr/bin/php5, /usr/bin/php70 ...
/usr/bin/php5                                # php 명령어 위치 입력
```

**Debian/Ubuntu**

* 패키지 저장소\(Repository\) 등록

와탭 저장소\(Repository\)를 등록합니다.

```text
$ wget http://repo.whatap.io/debian/release.gpg -O -|sudo apt-key add -
$ wget http://repo.whatap.io/debian/whatap-repo_1.0_all.deb
$ sudo dpkg -i whatap-repo_1.0_all.deb
$ sudo apt-get update
```

* 패키지 설치

  ```text
  $ sudo apt-get install whatap-php
  ```

* PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\) 등록

PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\)를 자동으로 설치할 경우에 아래와 같이 적용합니다

```text
$ sudo /usr/whatap/php/install.sh

Input license key
xxxxxxxxxxxxxxxx                               # 발급된 라이선스 key 입력

Input whatap.server.host
192.x.x.x                                       # 발급된 서버 IP 입력
```

PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\)를 자동으로 인식하지 못하는 경우 아래와 같이 선택 설치를 진행해야 합니다. 주로 Apache 명령어\(apachectl, httpd, apache2\) 및 PHP 명령어\(CLI\)가 기본 경로\($PATH\)에 설정 되어 있지 않거나, 여러 개의 PHP가 설치되어 PHP 명령어\(CLI\)가 여러 개일 경우에 \(php5, php70, php-zts, zts-php…\) 실제로 적용하고 있는 버전을 선택하여 진행합니다.

```text
$ sudo /usr/whatap/php/install.sh manual

Input license key
xxxxxxxxxxxxxxxx                          # 발급된 라이선스 key 입력

Input whatap.server.host
192.x.x.x                                  # 발급된 서버 Ip 입력

Input : which apache or php-fpm ex)/usr/sbin/httpd, /usr/sbin/apache2, /usr/sbin/php-fpm ...
/usr/sbin/httpd                           # apache 및 php-fpm 명령어 위치 입력

Input : which php ex) /usr/bin/php, /usr/bin/php5, /usr/bin/php70 ...
/usr/bin/php5                             # php 명령어 위치 입력
```

**패키지 설치 확인**

**PHP 확장 모듈**

PHP 추가 INI 경로에 whatap.ini 생성되어 있는지 확인합니다.

```text
$ find / | grep whatap.ini
```

PHP 확장 모듈\(PHP Extension module\) 경로에 whatap.so 파일 생성되어 있는지 확인합니다.

```text
$ find / | grep whatap.so
```

PHP 확장 모듈\(PHP Extension module\) 실행되고 있는지 확인합니다.

```text
$ sudo php -m

[PHP Modules]
bz2
calendar
Core
ctype
curl
date
…
whatap                  # whatap 모듈 실행 확인
…
[Zend Modules]
```

whatap-php 서비스\(Service\) 상태를 확인합니다.

```text
$ service whatap-php status
```

**실행**

**애플리케이션 재기동**

설치가 완료된 후 Apache 또는 PHP-FPM서비스\(Service\)를 재시작 하면 설정된 PHP 확장 모듈\(PHP Extension module\) whatap.so 파일이 로딩됩니다.

**whatap-php 서비스\(Service\) 재시작**

whatap-php 서비스\(Service\)가 실행 중이지 않거나 오류가 발생한 경우 재시작 합니다.

```text
$ sudo service whatap-php restart
```

**업데이트**

패키지 업데이트는 기존 설정을 유지한 채로 PHP 모니터링 서비스를 업데이트합니다. 0.2.7 이후 버전부터 정상적인 업데이트가 지원됩니다. 이전 버전은 삭제 후 설치를 진행해야 합니다.

**Redhat/CentOS**

패키지 정보 갱신을 위해 캐시 정보를 삭제합니다.

```text
$ yum clean all
```

Apache 또는 PHP-FPM서비스\(Service\)를 중지합니다.

whatap-php 패키지를 업데이트 합니다. $ yum update whatap-php

Apache 또는 PHP-FPM서비스\(Service\)를 시작합니다

**Debian/Ubuntu**

패키지 정보 갱신을 위해 캐시 정보를 갱신합니다.

```text
$ sudo apt-get update
```

Apache 또는 PHP-FPM서비스\(Service\)를 중지합니다.

whatap-php 패키지를 업데이트 합니다.

```text
$ sudo apt-get install --only-upgrade whatap-php
```

Apache 또는 PHP-FPM서비스\(Service\)를 시작합니다

**중지**

**일시 중지**

**PHP 확장 모듈\(PHP Extension module\) 중지**

whatap.ini 파일의 ‘extension=’ 구문을 주석처리 합니다.

수동 설정으로 php.ini 에 직접 설정한 경우도 동일하게 ‘extension=’ 구문을 주석처리 합니다. 주석은 세미콜론\( ; \) 으로 설정합니다.

```text
$ sudo vi whatap.ini

extension=whatap.so

;주석
;extension=whatap.so
```

**whatap-php 서비스\(Service\) 중지**

```text
$ sudo service whatap-php stop
```

**에이전트 삭제**

설치 스크립트를 이용하여 트레이서\(PHP Extension module\) 및 whatap-php 서비스\(Service\)를 삭제합니다.

이후 패키지\(yum, apt-get\) 삭제를 진행하고 필요에 따라서 /usr/whatap/php 아래에 로그 파일 및 기타 파일을 삭제합니다.

**PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\) 삭제**

```text
$ /usr/whatap/php/install.sh remove
```

**패키지 삭제**

* Redhat/CentOS

  ```text
  $ sudo yum remove whatap-php
  ```

* Debian/Ubuntu

  ```text
  $ sudo apt-get purge whatap-php
  ```

* /usr/whatap/php 디렉토리 삭제

#### 로그 {#user-content-로그}

**로그파일 종류**

로그파일은 2가지로 종류는 다음과 같습니다.

* whatap-boot-\[DATE\].log : 데이터 수집 로그
* whatap-install-\[DATE\].log : install.sh 실행 로그

**정상 동작 확인**

애플리케이션 서버를 기동 또는 재기동 한 뒤, 애플리케이션 서버 로그 및 에이전트 로그를 확인하여 PHP 모니터링 서비스의 정상 기동 여부를 확인합니다.apache/error\_log

```text
[Fri Nov 24 11:13:03 2017] [notice] Apache/2.2.15 (Unix) DAV/2 PHP/5.4.45 configured -- resuming normal operations
[Fri Nov 24 15:24:09 2017] [notice] caught SIGTERM, shutting down
[Fri Nov 24 15:24:09 2017] [notice] suEXEC mechanism enabled (wrapper: /usr/sbin/suexec)
[Fri Nov 24 15:24:09 2017] [notice] Digest: generating secret for digest authentication ...
[Fri Nov 24 15:24:09 2017] [notice] Digest: done
WA001 Whatap APM started
```

/usr/whatap/php/logs/whatap-boot-xxx.log

```text
2017/11/27 15:49:15 [WA214] Config: /etc/php.d/whatap.ini
2017/11/27 15:49:15
2017/11/27 15:49:15 ## OPEN LOG FILE  boot  0.3.0.20170929   20171127 06:49:15.44 ##
2017/11/27 15:49:15
2017/11/27 15:49:15 [WA827] 0xc4204ba460
2017/11/27 15:49:15 [WA214] Config: /etc/php.d/whatap.ini
2017/11/27 15:49:15 [WA171] PCODE=1234569399OID=-1182161871ONAME=d54FPHP-3-15-httpd
2017/11/27 15:49:15 [WA174] Net TCP: Connect to121.134.69.246:6600
2017/11/27 15:49:16 [WA632] Net UDP: Try to.... localhost:6600
2017/11/27 15:49:16 [WA635] Net UDP: Listener localhost:6600
```

#### 설치 에러 대응 {#user-content-설치-에러-대응-2}

**PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\) 수동 설정**

PHP 확장 모듈\(PHP Extension module\) , whatap-php 서비스\(Service\) 설치 및 선택 설치\(install.sh \)가 정상적으로 이루어 지지 않을 경우 수동으로 설정하는 방법을 설명합니다. PHP 컴파일\(Compile\) 설치 등의 이유로 환경 정보를 확인 할 수 없는 경우 사용합니다.

**whatap.ini 생성**

```text
$ cp /usr/whatap/php/template.ini /usr/whatap/php/whatap.ini
$ vi /usr/whatap/php/whatap.ini

# 상단에 내용 추가
; Enable whatap extension module
extension=whatap.so
whatap.license=            # 발급된 라이선스 key
whatap.server.host=        # 발급된 서버 IP
whatap.app_name=           # 웹서버 구분 APHP, FPHP (apache : APHP, php-fpm : FPHP)
whatap.app_process_name=   # apache, php-fpm 의 프로세스 이름(httpd,php-fpm)
```

| 설정 | 설명 |
| :--- | :--- |
| whatap.license | 프로젝트 &gt; 관리 &gt; 에이전트 설치 페이지에서 발급된 라이선스 키를 확인할 수 있습니다. |
| whatap.server.host | 프로젝트 &gt; 관리 &gt; 에이전트 설치 페이지에서 발급된 서버 IP를 확인할 수 있습니다. |
| whatap.app\_name | Apache 서버는 ‘APHP’, php-fpm 은 ‘FPHP’를 사용합니다. |
| whatap.app\_process\_name | Apache 또는 php-fpm 의 실행 프로세스 이름 설정으로 정확한 프로세스명 입력하면, 해당 프로세스에 대한 사용 메모리를 수집합니다. 예\) httpd, apach2, php-fpm, php-fpm 등. |

**PHP 명령어\(CLI\) 경로 확인**

```text
$ which php

/usr/bin/php
```

**whatap-php 서비스\(Service\) 환경 변수 설정**

$WHATAP\_PHP\_BIN 환경 변수에 PHP CLI 명령어의 경로를 설정합니다.

```text
$ sudo vi /etc/init.d/whatap-php

export WHATAP_PHP_BIN=         # PHP 명령어 위치(/usr/bin/php)
```

**PHP API 버전 확인**

$WHATAP\_PHP\_BIN 환경 변수에 PHP CLI 명령어의 경로를 설정합니다.

```text
$ sudo php -i | grep 'PHP API'

PHP API => 20100412
```

**PHP ZTS\(Zend Thread Safe\) 지원 여부 확인**

apache

```text
$ sudo apachectl -V | grep MPM

Server MPM: Prefork       	# ZTS 지원 안함
Server MPM: Worker       	# ZTS 지원
```

PHP-FPM

```text
$ sudo php-fpm -i | grep Thread

Thread Safety => disabled       	# ZTS 지원 안함
Thread Safety => enabled       	# ZTS 지원
```

**PHP 확장 모듈\(PHP Extension module\) 경로 확인 및 설정**

**PHP 확장 모듈\(PHP Extension module\) 경로 확인**

```text
$ sudo php -i | grep extension_dir

extension_dir => /usr/lib64/php/modules => /usr/lib64/php/modules
```

**PHP 확장 모듈\(PHP Extension module\) 설정**

PHP API 버전, PHP ZTS 지원 여부를 확인하여 환경에 적합한 라이브러리를 선택하여 PHP 확장 모듈\(PHP Extension module\) 경로에 whatap.so 파일명으로 복사합니다.

* PHP ZTS를 지원할 경우 - whatap\_zts\_\[PHP API 버전\].so
* PHP ZTS를 지원하지 않을 경우 - whatap\_\[PHP API 버전\].so

  ```text
  $ sudo cp /usr/whatap/php/modules/x64/whatap_20100412.so /usr/lib64/php/modules/whatap.so
  ```

**whatap-php 서비스\(Service\) 환경 변수 설정**

$WHATAP\_PHP\_EXT\_HOME 환경변수에 PHP 확장 모듈 경로를 설정합니다.

$WHATAP\_PHP\_EXT\_SRC 환경변수에 와탭 라이브러리 전체 파일 경로를 설정합니다.

```text
$ sudo vi /etc/init.d/whatap-php

export WHATAP_PHP_EXT_HOME=   # PHP Extension 경로(/usr/lib64/php/modules)
export WHATAP_PHP_EXT_SRC=    # 와탭 라이브러리 경로 및 파일명
                              # (/usr/whatap/php/modules/x64/whatap_20100412.so)]
```

**whatap.ini 설정**

**PHP 추가 ini 설정 경로 확인**

```text
$ sudo php -i | grep '.ini files'

Scan this dir for additional .ini files => /etc/php.d
```

whatap.ini를 해당 경로에 복사합니다.

```text
$ sudo cp /usr/whatap/php/whatap.ini /etc/php.d/whtap/ini
```

**PHP 추가 ini 설정 경로 확인 불가**

PHP 컴파일\(Compile\) 설치 옵션 ‘--with-config-file-scan-dir=PATH‘이 설정 안된 경우에 발생합니다.

```text
$ sudo php -i | grep '.ini files'

Scan this dir for additional .ini files => (none)
```

whatap.ini 파일 내용을 php.ini 마지막에 추가합니다.

```text
$ php -i | grep 'php.ini'

Loaded Configuration File => /etc/php.ini

$ sudo vi php.ini

# 파일 마지막에 추가
[whatap]
Enable whatap extension module
extension=whatap.so
whatap.ext.error_enabled=true
whatap.ext.exception_enabled=true
whatap.trace_user_enabled=true
whatap.trace_user_using_ip=false
```

이외 옵션은 /usr/whatap/php/whatap.ini 를 사용합니다.

**whatap-php 서비스\(Service\) 환경 변수 설정**

$WHATAP\_CONFIG\_HOME 환경변수에 whatap.ini 경로를 설정합니다.

PHP 추가 ini 경로를 확인 할 수 없는 경우 whatap.ini를 생성한 /usr/whatap/php 경로를 설정합니다.

```text
$ sudo vi /etc/init.d/whatap-php

export WHATAP_CONFIG_HOME=      # whatap.ini 경로(/etc/php.d)
```

**서비스 재시작**

Apache 및 PHP-FPM 서비스\(Service\)를 재시작 합니다.

whatap-php 서비스\(Service\)를 재시작 합니다.

**Error: Not found PHP API**

PHP 명령어\(CLI\)를 찾지 못하는 경우 발생합니다.

PHP 명령어\(CLI\)의 위치를 정확히 찾고, ‘PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\) 선택 설치’ 항목을 진행합니다.PHP API 버전 정보 확인

```text
$ sudo php -i | grep 'PHP API'

PHP API => 20100412
```

**Error: Not found PHP ini directory**

PHP 환경 중 ‘Scan this dir for additional .ini files’ 항목의 값을 확인 하지 못하는 경우 발생합니다. PHP 컴파일\(Compile\) 설치 옵션 ‘--with-config-file-scan-dir=PATH’ 이 설정 안된 경우에 해당 환경정보가 없습니다. PHP 명령어의\(CLI\) 경로를 정확히 찾고, ‘PHP 확장 모듈\(PHP Extension module\) 및 whata-php 서비스\(Service\) 수동 설정’ 항목을 진행합니다.

```text
$ sudo php -i | grep '.ini files'

Scan this dir for additional .ini files => (none)
```

**응답 시간 분포도 \(히트맵\)에 트랜잭션이 표시되지 않는 경우**

CPU, Memory의 그래프는 표기 되지만 응답 시간 분포도\(히트맵\)가 표기 되지 않는 현상은 에이전트가 수집서버와 정상적으로 연결 되었지만, 트레이서가 정상적으로 PHP 확장 모듈\(PHP Extension module\)로 적용되지 않았거나, 설정 후 Apache 및 PHP-FRPM 서비스\(Service\)를 재시작 하지 않은 경우에 발생합니다.

**PHP 확장 모듈\(PHP Extension module\) 확인**

```text
$ sudo php -m

 [PHP Modules]
bz2
calendar
Core
ctype
curl
date
…
whatap                 # 와탭 모듈 로드 확인
…
[Zend Modules]
```

PHP 확장 모듈\(PHP Extension module\) 적용을 확인 한 경우 Apache 및 PHP-FRPM 서비스\(Service\)를 재시작 합니다. 적용이 안된 경우는 정상 설치 되지 않은 것으로 whatap.so 또는 whatap.ini 파일 경로가 PHP 환경과 일치하는 지 확인합니다. ‘PHP 명령어\(CLI\) 경로 확인,’ PHP 확장 모듈\(PHP Extension module\) 경로 확인’, ‘PHP 추가 ini 설정 경로 확인’ 을 확인합니다.

#### FAQ {#user-content-faq-2}

#### 제약 사항 {#user-content-제약-사항-2}

#### 호환성 목록 {#user-content-호환성-목록-1}

**운영체제**

* Redhat/CentOS 64bit 6.x 이상
* Ubuntu 64bit 12.04 이상

**PHP**

* 5.2, 5.3, 5.4, 5.5, 5.6, 7.0, 7.1
* Non Tread Safe 방식 지원
* Tread Safe 방식 지원

### Python 애플리케이션 모니터링 {#user-content-python-애플리케이션-모니터링}

#### 에이전트 실행 및 모니터링 개요 {#user-content-에이전트-실행-및-모니터링-개요-2}

와탭 Python 애플리케이션 모니터링은 Python 기반 웹 애플리케이션 서버 모니터링 서비스를 제공합니다.

**에이전트 구성**

에이전트의 구성은 수집 서버, 에이전트, 그리고 수집서버로 이루어집니다.

* 수집서버
  * 에이전트가 수집한 애플리케이션의 성능 데이터를 수집, 저장 및 통계 정보 추출하고 이를 사용자에 효율적인 방법으로 제공합니다. 수집서버는 지역\(Region\)별로 설정이 가능합니다. 지역\(Region\)별로 수집서버의 주소가 다르게 할당 되므로 사용자가 선택한 지역\(Region\)에 따라 수집서버 주소는 다를 수 있습니다. 지역\(Region\) 선택은 프로젝트 생성시에 함께 설정합니다.
* 에이전트
  * 애플리케이션 서버에 설치되어, 애플리케이션 성능 데이터를 수집하여 서버로 전송합니다.
* 트레이서
  * 애플리케이션 코드에서 프로파일링 데이터를 추적합니다.
* 네트워크
  * 와탭 모니터링 에이전트는 모니터링 정보를 수집하여 서버에 데이터 전송하기 위하여 외부통신\(TCP\)을 위한 6600포트내부통신\(UDP\)을 위한 6600포트를 사용합니다. 내부 포트가 충돌이 나는 경우, net\_udp\_port=xxx 옵션으로 포트를 변경 할 수 있습니다.

[![530](https://github.com/jinronara/deleteme_2/raw/master/images/530.png)](https://github.com/jinronara/deleteme_2/blob/master/images/530.png)

**에이전트 구성 파일**

에이전트 구성 파일의 종류는 다음과 같습니다.

| 파일명 | 설명 |
| :--- | :--- |
| whatap.conf | 에이전트 설정 파일 |
| plugin.json | 플러그인 옵션에서 참조하는 파일 |
| paramkey.txt | 보안키를 필요로 하는 옵션에서 참조하는 파일 |

**설정 파일**

* 파일명: whatap.conf
  * 에이전트 설정 기본 필수 파일입니다. 에이전트와 관련된 옵션은 모두 whatap.conf에서 설정이 가능합니다.

**플러그인 파일**

* 파일명: plugin.json
  * 기본적으로 제공하는 트랜잭션 추적 모듈 이외에 사용자가 메뉴얼하게 모듈을 추가 할때 참고 하는 파일입니다. 형식에 맞게 내용을 추가하면 특정 모듈의 데이터를 추적할 수 있습니다. 옵션은 whatap.conf에서 설정이 가능합니다. 관련 옵션은 다음과 같습니다.
* plugin default: false

**보안키 파일**

* 파일명: paramkey.txt
  * 추적한 트랜잭션의 프로파일정보로 수집한 HTTP와 SQL데이터의 파라미터 정보를 확인 하는데 사용합니다. 보안키를 파일에 저장하고 실제 수집된 데이터를 브라우저에서 확인 하고자 할 때 파일에 저장해 둔 보안키를 입력해야 조회 할 수 있습니다. 파일의 내용을 변경하여 보안키 수정이 가능하다. 옵션은 whatap.conf에서 설정이 가능합니다. 관련 옵션은 다음과 같습니다.
* profile\_http\_parameter\_enabled default: false

**에이전트 이름 식별**

와탭은 모니터링 정보 수집 대상인 애플리케이션 서버 식별을 위한 정보로 기본적으로 애플리케이션 서버로부터 수집한 정보를 활용합니다. 기본적으로 활용하는 정보는 애플리케이션 서버 종류, 애플리케이션 서버의 IP, 서비스 포트를 조합하여 애플리케이션 서버를 고유 식별자로 사용하게 되며 필요에 따라 사용자가 지정한 명칭을 사용하거나 패턴을 변경하여 사용하는 것도 가능합니다. 이때에는 꼭 고유한 값이어야만 합니다. 애플리케이션 서버로부터 추출한 정보를 활용하는 이유는 애플리케이션 서버 정지, 네트워크 단절 또는 에이전트 문제로 인한 수집 서버와 에이전트의 통신 단절 상태가 복구되었을 경우, 재접속된 에이전트로부터 송신되는 정보가 기존 에이전트로부터 송신된 정보와의 연속성을 유지하기 위해서 입니다. 와탭이 애플리케이션 서버를 식별하기 위해 사용하는 기본 패턴은 다음과 같습니다.

* default: {type}-{ip2}-{ip3}-{process}

기본 패턴에 대한 변경은 whatap.conf에서 설정에서 가능합니다.

* object\_name default: {type}-{ip2}-{ip3}-{process}

Table 1. 패턴 옵션

| 설정 | 설명 |
| :--- | :--- |
| type | app\_name |
| ip\# | Ip를 .으로 나누었을 때 \#번째 자리\(0부터\) |
| process | app\_process\_name |
| hostname | 호스트 명 |

#### 에이전트 설치 및 패키지 업데이트/제거 {#user-content-에이전트-설치-및-패키지-업데이트-제거}

**설치**

**프로젝트 생성**

[![540](https://github.com/jinronara/deleteme_2/raw/master/images/540.png)](https://github.com/jinronara/deleteme_2/blob/master/images/540.png)

서버를 등록하기 위해 우선 프로젝트를 생성합니다. 추가 버튼을 선택하면 아래와 같이 프로젝트 생성 창이 나타납니다. PHP 아이콘을 선택한 뒤, 희망하는 프로젝트명과 데이터 서버 지역\(Region\), 소속하게 될 그룹을 선택한 뒤 프로젝트를 생성합니다.[![550](https://github.com/jinronara/deleteme_2/raw/master/images/550.png)](https://github.com/jinronara/deleteme_2/blob/master/images/550.png)

**라이선스 발급**

[![560](https://github.com/jinronara/deleteme_2/raw/master/images/560.png)](https://github.com/jinronara/deleteme_2/blob/master/images/560.png)

프로젝트 관리화면에서는 우선적으로 라이선스를 발급 받습니다. 라이선스 키는 프로젝트별로 귀속되기 때문에, 유출되거나 배포되어서는 안됩니다. 반드시 본인 프로젝트에 서버를 등록할 때에만 이용하시기 바랍니다.

**WHATAP\_HOME 기본 경로 설정**

로그와 설정파일 경로를 위한 $WHATAP\_HOME 경로를 지정해 주세요. `whatap` 디렉토리를 새로 생성하는 것을 권장합니다.

```text
$ export WHATAP_HOME=[PATH]
```

**라이선스 키 및 수집서버 설정**

다음 명령어를 실행하면 $WHATAP\_HOME에 지정한 경로에 바로 whatap.conf 파일이 생성 및 설정 됩니다.

```text
$ whatap-setting-config
 --host [HOST_ADDR]
 --license [LICENSE_KEY]
 --app_name [APPLICATION_NAME]
 --app_process_name [APP_PROCESS_NAME ex]uwsgi, gunicorn..]
```

**설정 확인**

다음과 같이 설정파일이 잘 생성되어 있는지 확인 해 주세요.

```text
$ cat $WHATAP_HOME/whatap.conf
```

**명령어 실행**

WHATAP\_AGENT시작 커맨드와 함께 애플리케이션 서버를 재시작해주세요.

```text
$ whatap-start-agent [YOUR_APPLICATION_START_COMMAND]
```

**애플리케이션 재 시작**

애플리케이션 서버가 실행되면 애플리케이션의 모니터링 정보를 수집하기 시작합니다.

**에이전트 프로세스 확인**

다음과 같은 명령어를 통하여 동작중인 와탭 Python 에이전트 프로세스를 확인 할 수 있습니다.

```text
$ ps –ef | grep whatap_python
```

**에이전트 삭제**

에이전트 삭제를 원하는 경우, 다음 절차를 진행 해 주세요..

1. 애플리케이션 서버 재시작 시 함께 추가한 WHATAP\_AGENT시작 커맨드를 삭제 합니다.
2. whatap-stop-agent 명령어로 와탭 Python 에이전트 프로세스를 종료합니다.

   ```text
   $ whatap-stop-agent
   ```

3. 혹시 되지 않으시면 다음과 같이 프로세스를 종료시켜 주세요.

   ```text
   $ killall whatap-python
   ```

4. 프로세스가 정삭적으로 죽었는지에 대한 확인은 다음 명령어로 확인 가능합니다.

   ```text
   $ ps -ef|grep whatap_python
   ```

**패키지 설치 확인/업데이트/제거**

**패키지 설치 확인**

다음과 같은 명령어를 통하여 설치된 와탭 Python 에이전트 패키지를 확인 할 수 있습니다.

```text
$ pip list | grep whatap-python
```

**패키지 업데이트**

다음과 같은 명령어를 통하여 설치된 와탭 Python 에이전트 패키지를 업데이트 할 수 있습니다.

```text
$ pip install –U whatap-python
```

또는

```text
$ pip install –U whatap-python==[특정 버전]
```

**패키지 제거**

다음과 같은 명령어를 통하여 설치된 와탭 Python 에이전트 패키지를 제거 할 수 있습니다.

```text
$ pip uninstall whatap-python
```

**사용 예**

**기본**

예제

```text
$ whatap-start-agent python manage.py runserver
```

**uWSGI**

예제 1

```text
$ whatap-start-agent uwsgi --ini myapp.ini
```

예제 2

```text
description "uWSGI application server handling myapp"

start on runlevel [2345]
stop on runlevel [!2345]

exec whatap-start-agent [YOUR_APPLICATION_START_COMMAND]
또는
exec env WHATAP_HOME=[PATH] [절대 경로]/whatap-start-agent [YOUR_APPLICATION_START_COMMAND]
```

예제 3

```text
$ whatap-start-agent gunicorn myapp.wsgi
```

**Gunicorn**

예제 1

```text
NAME="uwsgi"
PATH=/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
DAEMON=/usr/local/bin/uwsgi

########## WHATAP_AGENT_CONF ##########
WHATAP_HOME=[PATH]
WHATAP_AGENT=[절대 경로]/whatap-start-agent
...
do_start(){
    env WHATAP_HOME=$WHATAP_HOME $WHATAP_AGENT [YOUR_APPLICATION_START_COMMAND]
}
```

예제 2

```text
description "Gunicorn application server handling myapp"

start on runlevel [2345]
stop on runlevel [!2345]

exec whatap-start-agent [YOUR_APPLICATION_START_COMMAND]
또는
exec env WHATAP_HOME=[PATH] [절대 경로]/whatap-start-agent [YOUR_APPLICATION_START_COMMAND]
```

예제 3

```text
NAME="gunicorn"
PATH=/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
DAEMON=/usr/local/bin/gunicorn

########## WHATAP_AGENT_CONF ##########
WHATAP_HOME=[PATH]
WHATAP_AGENT=[절대 경로]/whatap-start-agent
...
do_start(){
    env WHATAP_HOME=$WHATAP_HOME $WHATAP_AGENT [YOUR_APPLICATION_START_COMMAND]
}
```

**Supervisor**

예제

```text
[program:app-uwsgi]
environment = WHATAP_HOME=[PATH]
command = [절대 경로]/whatap-start-agent /usr/local/bin/uwsgi --ini /home/blog/backend/config/uwsgi.ini

[program:nginx-app]
command = /usr/sbin/nginx
```

**WSGI 애플리케이션 직접 구현**

예제

```text
import whatap

@whatap.register_app
def simple_app(environ, start_response):
    """Simplest possible application object"""
    status = '200 OK'
    response_headers = [('Content-type', 'text/plain')]
    start_response(status, response_headers)
    return ['Hello world!\n']
```

#### 에이전트 로그 {#user-content-에이전트-로그}

애플리케이션 서버가 실행되면 애플리케이션의 모니터링 정보를 수집하기 시작합니다. 로그의 위치는 $WHATAP\_HOME의 logs디렉토리에 다음과 같은 파일로 생성됩니다.

**로그파일 종류**

로그 파일은 2가지로 종류는 다음과 같습니다.

* whatap-boot-\[DATE\].log : 데이터 수집 로그
* whatap-hook.log : 데이터 수집 로그

**정상 동작 확인**

다음은 정상 동작하는 경우의 로그 예 입니다.

```text
_      ____       ______Python-AGENT
| | /| / / /  ___ /_  __/__ ____
| |/ |/ / _ \/ _ `// / / _ `/ _ \
|__/|__/_//_/\_,_//_/  \_,_/ .__/
                          /_/
Just Tap, Always Monitoring
WhaTap Python Agent version 0.1.33, 20171017

WHATAP_HOME: /Users/kimjihye/workspace/whatap/python-sample/whatap
Config: /Users/kimjihye/workspace/whatap/python-sample/whatap/whatap.conf
Logs: /Users/kimjihye/workspace/whatap/python-sample/whatap/logs
```

#### 설치 에러 대응 {#user-content-설치-에러-대응-3}

**Permission denied 에러 발생 시**

와탭 파이썬 모니터링을 사용하기 위해서는 다음과 같은 권한 필요 합니다.

* 와탭 설정을 위한 $WHATPA\_HOME/whatap.conf 파일의 읽기 및 쓰기 권한
* 와탭 로그를 위한 $WHATPA\_HOME/logs 디렉토리와 하위 파일의 읽기 및 쓰기 권한

권한 문제가 발생하는 경우\(Permission denied error\), 다음과 같이 $WHATPA\_HOME에 권한을 부여합니다.

```text
$ echo `sudo chmod -R 777 $WHATAP_HOME`
```

**프로젝트에 에이전트가 등록되지 않는 경우 모니터링 데이터 수집이 이루어지지 않는 경우**

로그 파일\($WHATAP\_HOME/logs/\)을 확인 한 후 각각의 문제에 대하여 다음과 같이 문제를 해결 할 수 있습니다.

* whatap-hook.log
  * CONF FILE ERROR: 설정파일 생성 권한이 없습니다. 파일을 만들어 주세요.
  * CONF READ ERROR: 설정파일은 있으나 리드권한이 없습니다. 권한을 주어야 합니다.
  * LOG FILE ERROR: 로그 디렉토리 생성 권한이 없이 없습니다. 디렉토리를 만들어 주세요.
  * LOGGING ERROR: 로그 디렉토리는 있으나, 쓰기 권한 없습니다. 권한을 주어야 합니다.
* whatap-boot-\[DATE\].log
  * license or whatp.server.host error: 라이선스키 또는 수집서버 주소가 잘못되었습니다

**포트 충돌이 발생하는 경우**

내부 통신을 하는 에이전트는 기본으로 UDP 6600포트를 사용합니다. 내부 포트가 충돌이 나는 경우, net\_udp\_port=xxx 옵션으로 포트를 변경 할 수 있습니다

**$WHATAP\_HOME 환경 변수가 설정되지 않는 경우**

**Apache HTTPD**

아파치로 웹 서버 구동하는 경우 환경변수 설정을 다음과 같이 해 주어야 합니다.

```text
<VirtualHost *:80>
    #ServerName
    #DocumentRoot

        SetEnv WHATAP_HOME "application path"
    # Directory
</VirtualHost>
```

**수동으로 환경변수 설정 하는 경우**

필요에 따라서는, 다음과 같이 수동으로 환경 변수를 설정 해 주어야 합니다.

```text
---
import os
os.environ.setdefault("WHATAP_HOME", [application path]")
import whatap
---
```

#### FAQ {#user-content-faq-3}

#### 제약 사항 {#user-content-제약-사항-3}

#### 호환성 목록 {#user-content-호환성-목록-2}

**운영체제**

* CentOS 64bit 6 이상
* Ubuntu 64bit 14 이상

**Python**

* Python 2.7 이상 & Python 3.3 이상

### 인프라 모니터링 {#user-content-인프라-모니터링}

#### 에이전트 실행 및 모니터링 개요 {#user-content-에이전트-실행-및-모니터링-개요-3}

와탭 인프라스트럭처 모니터링은 서버 성능 모니터링 서비스를 제공합니다.

**구성 파일**

**공통 구성 파일**

| 파일명 | 설명 |
| :--- | :--- |
| ChangeLog.txt | 에이전트의 버전 패치 내역 |
| whatap.conf | 서버의 데이터를 수집할 서버의 주소와 서버의 프로젝트 라이선스 키가 입력되는 파일 |

**Linux 구성 파일**

| 파일명 | 설명 |
| :--- | :--- |
| whatap\_infrad | 데이터 수집 및 전송용 에이전트 |
| whatap\_infrad.pid | 실행 중인 에이전트의 PID 값을 기록한 파일 |
| VERSION | 현재 설치된 에이전트의 버전이 기록된 파일 |

**Windows 구성 파일**

| 파일명 | 설명 |
| :--- | :--- |
| whatap\_infra.exe | 정보를 수집하고 수집된 정보를 서버로 전송하는 프로그램 |
| unins000.\* | 에이전트 삭제 파일 |
| whatap.ico | 와탭 인프라의 아이콘 이미지 |

**에이전트 이름 식별**

와탭은 모니터링 정보 수집 대상인 인프라 서버 식별을 위한 정보로 기본적으로 서버로부터 수집한 정보를 활용합니다. 기본적으로 활용하는 정보는 서버의 호스트명\(hostname\)이 됩니다.

* default: hostname

#### 에이전트 설치 및 패키지 업데이트/제거 {#user-content-에이전트-설치-및-패키지-업데이트-제거-1}

와탭 인프라스트럭처 모니터링 서비스를 이용하기 위해서는 모니터링 대상 서버에 와탭 인프라 모니터링 에이전트 설치해야 합니다. 와탭 인프라스트럭처 모니터링 에이전트 설치 방법은 whatap.io 사이트에서 제공하는 명령어를 수행하는 것만으로 설치가 완료됩니다.

**공통**

**프로젝트 생성**

[![570](https://github.com/jinronara/deleteme_2/raw/master/images/570.png)](https://github.com/jinronara/deleteme_2/blob/master/images/570.png)

서버를 등록하기 위해 우선 프로젝트를 생성합니다. 추가 버튼을 선택하면 아래와 같이 프로젝트 생성 창이 나타납니다. INFRASTRUCTURE 아이콘을 선택한 뒤, 희망하는 프로젝트명과 데이터 서버 지역, 소속하게 될 그룹을 선택한 뒤 프로젝트를 생성합니다.[![580](https://github.com/jinronara/deleteme_2/raw/master/images/580.png)](https://github.com/jinronara/deleteme_2/blob/master/images/580.png)

**라이선스 발급**

[![590](https://github.com/jinronara/deleteme_2/raw/master/images/590.png)](https://github.com/jinronara/deleteme_2/blob/master/images/590.png)

에이전트 설치 화면에서 라이선스를 발급 받습니다. 라이선스 키는 프로젝트별로 귀속되기 때문에, 유출되거나 배포되어서는 안됩니다. 반드시 본인 프로젝트에 서버를 등록할 때에만 이용하시기 바랍니다.

**Debian/Ubuntu**

**패키지 저장소\(Repository\) 등록**

와탭 저장소\(Repository\)를 추가합니다.

```text
$ wget http://repo.whatap.io/debian/release.gpg -O -|sudo apt-key add -
$ wget http://repo.whatap.io/debian/whatap-repo_1.0_all.deb
$ sudo dpkg -i whatap-repo_1.0_all.deb
$ sudo apt-get update
```

**인프라 모니터링 설치**

아래의 명령어를 입력하여 와탭 인프라 모니터링을 설치합니다.

```text
$ sudo apt-get install whatap-infra
```

**라이선스키 및 수집 서버 설정**

아래의 명령어에 발급받은 라이선스 키와 수집 서버 IP를 넣어 입력함으로써 설정을 합니다.

```text
$ echo "license=[라이선스 키]" |sudo tee /usr/whatap/infra/conf/whatap.conf
$ echo "whatap.server.host=[발급된 수집 서버 IP]" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
$ echo "createdtime=`date +%s%N`" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
sudo service whatap-infra restart
```

* 에이전트 설치 페이지에서 발급 받은 명령문에는 라이선스 키가 포함되어 있기 때문에 유출되거나, 배포되지 않도록 주의하시길 바랍니다.
* 에이전트는 수집 서버 주소로 정보를 전송합니다. 그러므로 에이전트가 설치된 서버는 TCP 아웃바운드 포트\(6600\)가 열려 있어야 합니다.

**Redhat/CentOS/Amazon-Linux**

**패키지 저장소\(Repository\) 등록**

와탭 저장소\(Repository\)를 추가합니다.

```text
sudo rpm --import http://repo.whatap.io/centos/release.gpg
sudo rpm -Uvh http://repo.whatap.io/centos/5/noarch/whatap-repo-1.0-1.noarch.rpm
```

**인프라 모니터링 설치**

아래의 명령어를 입력하여 와탭 인프라 모니터링을 설치합니다.

```text
sudo yum install whatap-infra
```

라이선스 수집 서버 설정

```text
$ echo "license=[라이선스 키]" |sudo tee /usr/whatap/infra/conf/whatap.conf
$ echo "whatap.server.host=[발급된 수집 서버 IP]" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
$ echo "createdtime=`date +%s%N`" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
sudo service whatap-infra restart
```

* 에이전트 설치 페이지에서 발급 받은 명령문에는 라이선스 키가 포함되어 있기 때문에 유출되거나, 배포되지 않도록 주의하시길 바랍니다.
* 에이전트는 수집 서버 주소로 정보를 전송합니다. 그러므로 에이전트가 설치된 서버는 TCP 아웃바운드 포트\(6600\)가 열려 있어야 합니다.

**Windows**

**에이전트 다운로드**

에이전트 설치 페이지에서 WINDOWS를 클릭합니다.[![600](https://github.com/jinronara/deleteme_2/raw/master/images/600.png)](https://github.com/jinronara/deleteme_2/blob/master/images/600.png)

whata\_infra.exe 파일을 다운받습니다. 보안 설정으로 인해 .exe형식의 파일을 받지 못할 경우를 대비하여 .zip 형식의 파일로도 다운받을 수 있습니다.

* 서버 보안을 위해 브라우저를 통한 직접 설치보다 다운로드 받은 설치 파일을 실행시키는 것을 권장합니다.

**에이전트 업로드**

인프라 모니터링을 설치할 서버에 접속하고, 다운로드 받은 에이전트 파일을 업로드합니다.

**에이전트 설치**

서버에서 업로드 받은 파일을 실행합니다.[![610](https://github.com/jinronara/deleteme_2/raw/master/images/610.png)](https://github.com/jinronara/deleteme_2/blob/master/images/610.png)

해당 입력란에 발급받은 라이선스 키와 데이터 서버 주소\(IP\)를 입력합니다. 이후 설치가 완료되면 아래 그림과 같은 화면을 볼 수 있으며, 에이전트가 자동적으로 모니터링을 시작합니다. 버튼을 눌러 설치를 완료합니다.

* 에이전트는 수집 서버 주소로 정보를 전송합니다. 그러므로 수집 서버 주소로 가는 TCP 아웃바운드 포트\(6600\)가 차단되어 있으면 안됩니다.

[![620](https://github.com/jinronara/deleteme_2/raw/master/images/620.png)](https://github.com/jinronara/deleteme_2/blob/master/images/620.png)

**알림 일시 정지**

서버는 운영 중에 확장/유지보수/문제해결/단순 재시작 등의 이유로 잠시 정지해야 할 필요가 있습니다. 이럴 경우 불필요한 오탐을 방지하기 위해 서비스를 잠시 일시정지가 가능합니다.

* 주의: 서비스 일시정지 시에도 요금은 청구됩니다,

[![630](https://github.com/jinronara/deleteme_2/raw/master/images/630.png)](https://github.com/jinronara/deleteme_2/blob/master/images/630.png)

모니터링 중인 서버들 중 일시정지하고자 하는 서버를 선택합니다. 일시정지하고자 하는 서버 선택 후 우측 상단에 있는 액션을 클릭하면 드롭다운 메뉴가 나오는 것이 확인 가능합니다. 해당 메뉴에서 일시정지 버튼을 클릭할 경우 알림이 나가지 않습니다.

* 일시정지 기간 동안에는 데이터가 수집되지만 알림이 발생하지 않습니다.

**알림 재시작**

서버 작업 완료 후 알림 발송을 재개하기 위해서는 재시작 하길 원하는 서버를 선택 후 액션을 클릭하여 나오는 드롭다운 메뉴에서 재시작 버튼을 클릭하여 알림 발송을 재개합니다.

**해지**

모니터링이 더 이상 필요하지 않을 경우 와탭 에이전트를 손쉽게 해지할 수 있습니다. 해지를 희망하는 서버를 선택한 후, 액션 버튼을 클릭하여 나오는 드롭다운 메뉴에서 해지 버튼을 누르면 아래 그림과 같은 팝업창을 확인 할 수 있습니다.[![630](https://github.com/jinronara/deleteme_2/raw/master/images/630.png)](https://github.com/jinronara/deleteme_2/blob/master/images/630.png)

해당 팝업 창에서 해지를 누를 경우 서버가 해지됩니다.

* 주의 : 모니터링 해지 시 해당되는 수집 서버에 저장된 데이터가 즉시 사라져 보고서와 같은 서비스를 받으실 수 없습니다. 따라서 삭제 전 신중하게 결정하여 해지해주시길 바랍니다.

**제거**

와탭 콘솔상에서 서버 해지를 완료하였다면, 서버 상에서도 에이전트 삭제가 필요합니다.

**Debian/Ubuntu**

```text
$ apt-get remove whatap-infra
```

* 남아있는 설정파일은 /usr/whatap에 있습니다. 해당 whatap 폴더를 지워주시면 됩니다.

**Redhat/CentOS/Amazon-Linux**

```text
$ yum remove whatap-infra
```

* 남아있는 설정파일은 /usr/whatap에 있습니다. 해당 whatap 폴더를 지워주시면 됩니다.

**Windows**

제어판 → 프로그램 추가/제거에서 인프라 모니터링을 찾아서 삭제하시거나 와탭 설치 경로인 C:\Program Files\WhatapInfra 에서 unins000.exe를 실행하여 삭제하셔도 됩니다.

#### FAQ {#user-content-faq-4}

**업그레이드**

**윈도우 버전 업그레이드**

기존 와탭 인프라 에이전트 프로그램을 삭제하지 말고 설치 파일을 실행하면 자동으로 업그레이드 됩니다.

**Ubuntu 계열**

아래와 같이 실행합니다.

```text
apt-get update
apt-get install whatap-infra
```

**Redhat 계열**

아래와 같이 실행합니다.

```text
yum check-update
yum install whatap-infra
```

**인터넷 연결이 안되는 서버에 설치**

**Windows OS**

아래 주소에서 다운받으실 수 있습니다.

[http://repo.whatap.io/windows/whatap.zip](http://repo.whatap.io/windows/whatap.zip)

**Ubuntu OS**

[http://repo.whatap.io/debian/unstable/whatap-infra\_{x}.{x}.{x}\_amd64.deb](http://repo.whatap.io/debian/unstable/whatap-infra_%7Bx%7D.%7Bx%7D.%7Bx%7D_amd64.deb)

[http://repo.whatap.io/debian/unstable/whatap-infra\_{x}.{x}.{x}\_i386.deb](http://repo.whatap.io/debian/unstable/whatap-infra_%7Bx%7D.%7Bx%7D.%7Bx%7D_i386.deb)

**CentOS/RedHat/AmazonLinux**

[http://repo.whatap.io/centos/6/x86\_64/](http://repo.whatap.io/centos/6/x86_64/) whatap-infra-{x}.{x}-{x}.86\_64.rpm

[http://repo.whatap.io/centos/6/i386/](http://repo.whatap.io/centos/6/i386/) whatap-infra-{x}.{x}-{x}.i386.rpm

[http://repo.whatap.io/centos/7/x86\_64/](http://repo.whatap.io/centos/7/x86_64/) whatap-infra-{x}.{x}-{x}.86\_64.rpm

**최신버젼 확인**

**Ubuntu/Debian**

아래 명령을 터미널에서 실행합니다.

```text
apt-cache showpkg whatap-infra
```

**CentOS/RedHat/AmazonLinux**

아래 명령을 터미널에서 실행합니다.

```text
yum info whatap-infra
```

#### 설치 에러 대응 {#user-content-설치-에러-대응-4}

**설치 후 서버 목록에 표시되지 않을 때**

**Windows**

Cmd 창에서 아래 명령을 수행 하면 오류 원인을 파악할 수 있습니다.

```text
“C:\Program Files\WhatapInfra\whatap_infra.exe” –whatapip {수집서버 IP} –license {라이선스 문자열} test
```

**Linux**

터미널에서 아래 명령을 수행하면 오류 원인을 파악 할 수 있습니다.

```text
/usr/whatap/infra/whatap_infrad –whatapip {수집서버 IP}—license {라이선스 문자열} test
```

#### 제약 사항 {#user-content-제약-사항-4}

제약사항 없음

#### 호환성 목록 {#user-content-호환성-목록-3}

* Debian 7.0 이상
* Ubuntu 12.04 이상
* CentOS 6 이상
* RHEL 6 이상
* Amazon Linux
* Windows Server 2008 R2 SP2 이상

### 데이터베이스 모니터링 \(준비중\) {#user-content-데이터베이스-모니터링-준비중}

#### 모니터링 에이전트 개요 {#user-content-모니터링-에이전트-개요-1}

**에이전트 설치 방식 개요**

**구성 파일**

**에이전트 실행 및 모니터링 개요**

#### 에이전트 설치/실행/업데이트/중지 {#user-content-에이전트-설치-실행-업데이트-중지-3}

**공통**

**회원 가입**

**서비스 선택**

**프로젝트 생성**

**라이선스 발급**

**설치**

**실행**

**업데이트**

**중지**

### 소프트웨어 프록시 \(준비 중\) {#user-content-소프트웨어-프록시-준비-중}

#### 개요 {#user-content-개요}

#### 환경 {#user-content-환경}

#### 구성파일 {#user-content-구성파일}

#### 설치 {#user-content-설치-6}

#### 설정 {#user-content-설정-1}

#### 실행 {#user-content-실행-6}

#### 중지 {#user-content-중지-4}

### 설치형 서버 구축 \(준비 중\) {#user-content-설치형-서버-구축-준비-중}

#### 수집 서버 설치 {#user-content-수집-서버-설치}

**수집 서버 권장 사양**

**설치 작업 절차**

**H2 서버 구축**

#### 운용 사항 {#user-content-운용-사항}

