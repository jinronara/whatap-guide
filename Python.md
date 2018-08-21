## Python 애플리케이션 모니터링 {#user-content-python-애플리케이션-모니터링}

### 소개 {#user-content-소개}

해당 가이드는 Python 애플리케이션 모니터링을 할 때에 설정할 수 있는 옵션에 대해 설명합니다. \(\*\) 표시가 있는 옵션은 애플리케이션을 재시작 하여야만 적용되는 옵션입니다.

### 에이전트 네트워크 통신에 관한 설정 {#user-content-에이전트-네트워크-통신에-관한-설정}

license

에이전트 설치시 서버로부터 부여받은 라이센스를 지정합니다. 라이센스에는 에이전트가 속한 프로젝트와 보안 통신을 위한 암호키를 포함하고 있습니다.

* Default : \[**NONE**\]
* Type : String

whatap.server.host

에이전트가 수집한 데이터를 전송할 서버를 지정합니다. 수집서버 이중화로 2개 이상의 IP를 가진 경우 콤마\(,\)로 분리하여 지정할 수 있습니다. 지정된 IP 에는 수집서버 proxy 데몬이 리스닝 상태로 서비스 되어야 합니다.

* Default : \[**127.0.0.1,127.0.0.1**\]
* Type : ip\_address

whatap.server.port

수집서버 PORT 를 지정합니다. 포트는 하나만 지정할 수 있으므로 whatap\_server\_host 에 지정된 수집서버들은 동일 PORT 를 사용해야 합니다.

* Default : \[**6600**\]
* Type : tcp\_port

### 에이전트 네트워크 내부 통신에 관한 설정 {#user-content-에이전트-네트워크-내부-통신에-관한-설정}

와탭 에이전트는 수집한 데이터를 UDP를 거쳐 TCP를 통해 서버로 전송을 하는데, 처음 UDP서버의 포트를 지정할 수 있습니다. 기본값으로 제공되는 6600포트가 사용 중일 때 이 옵션을 사용합니다.

* Default : \[**6600**\]
* Type : tcp\_port

### 에이전트 네트워크 외부 통신에 관한 설정 {#user-content-에이전트-네트워크-외부-통신에-관한-설정}

tcp\_so\_timeout

수집서버와 통신하는 TCP세션의 Socket Timeout 값을 지정합니다.

* Default : \[**60000**\]
* Type : MiliSecond

tcp\_connection\_timeout

수집서버와 통신하는 TCP세션의 Connection Timeout 값을 지정합니다.

* Default : \[**5000**\]
* Type : MiliSecond

net\_send\_max\_bytes

에이전트가 데이터를 수집하고 네트워크로 한번에 전송할 수 있는 최대 바이트 크기입니다.

* Default : \[**5242880**\]
* Type : Byte

net\_send\_buffer\_size

데이터 전송을 하기 위해 가지고 있는 최대 바이트 크기입니다.

* Default: \[**1024**\]
* Type: byte

### 애플리케이션 등록에 관한 설정 {#user-content-애플리케이션-등록에-관한-설정}

object\_name

애플리케이션을 식별하는 에이전트 이름\(ONAME\)체계입니다. ONAME을 토대로 OID가 생성됩니다.

* Default : \[**{type}-{ip2}-{ip3}-{process}**\]
* Type : String
* remark: 재기동 필요 \(Apache 및 PHP-FPM\)

| 명칭 | 설명 |
| :--- | :--- |
| {type} | whatap.app\_name 에 설정된 값을 사용합니다. |
| {ip\#} | IP를 나누었을 때 \#번째 자리를 사용합니다. |
| {process} | whatap.app\_process\_name 에 설정된 값을 사용합니다. |
| {hostname} | 서버 호스트명을 사용합니다. |

app\_name

애플리케이션을 식별하는 에이전트 이름\(ONAME\)체계에 사용되는 애플리케이션 명. object\_name의 {type}에 해당하는 값이다.

* Default : \[**NONE**\]
* Type : String

app\_process\_name

애플리케이션을 식별하는 에이전트 이름\(ONAME\)체계에 사용되는 애플리케이션 프로세스 명. 애플리케이션 서버의 CPU, Heap Memory등을 수집할 대상 프로셋를 설정합니다. object\_name의 {process}에 해당하는 값이다.

* Default : \[**NONE**\]
* Type : String

auto\_oname\_enabled

서버에 등록될 에이전트 이름\(oname\)을 서버로부터 자동 부여 받는 기능을 활성화 합니다. 적용 시, -Dwhatap.name, -Dwhatap.oname 옵션은 무시됩니다. 수집 서버와의 통신을 통해 oname 을 부여 받은 이후, 에이전트의 일반적인 동작을 개시합니다.

* Default : \[**false**\]
* Type : Boolean

auto\_oname\_prefix

에이전트 이름을 서버로부터 자동 부여할 때 에이전트 이름의 prefix, 보통 업무 명을 사용합니다. prefix 일련번호 1~\) 부여됩니다.

* Default : \[**agent**\]
* Type : String

auto\_oname\_reset

서버로 부터 새로운 에이전트 이름을 부여받기 위해서 수정합니다. 에이전트 이름을 자동 부여하면 what.oname 이라는 시스템 환경 변수에 셋트됩니다. 한번 셋트되면 자바 인스턴스가 재기동 될 때까지 유지 되는데 리셋을 원할 때 auto\_oname\_reset 값을 수정합니다.\(현재 설정 값과 다른 값으로 변경하면 적용됩니다.\)

* Default : \[**0**\]
* Type : Int

### 에이전트 기능 제어에 관한 설정 {#user-content-에이전트-기능-제어에-관한-설정}

enabled

전체 기능을 활성화 합니다. false인 경우에도 서버와 최소한의 통신을 유지하기 위한 정보는 전송됩니다.

* Default : \[**true**\]
* Type : Boolean

plugin

기본적으로 제공하는 트랜잭션 추적 모듈 이외에 사용자가 원하는 모듈 추적에 대한 기능을 플러그인 형태로 제공한다. 옵션을 활성화 하면 $WHATAP\_HOME으로 지정한 경로에 plugin.json 파일이 자동 생성되며, 형식에 맞게 내용을 추가하면 사용자가 메뉴얼하게 모듈을 추가하여 특정 모듈의 데이터를 추적할 수 있다. 사용자 별로 원하는 모듈을 추적하고자 할 때 활용한다. 기본 모듈과 중복이 되는 경우, 사용자의 설정이 우선시 된다. \[module\_name\]: 추적하고자 하는 대상의 모듈 명. import 하는 모듈 명 이기도 하다.

* Default : \[**false**\]
* Type : Boolean

| 설정 | 설명 |
| :--- | :--- |
| \[class\_name\] | 추적하고자 하는 대상의 클래스 명이 없다면 ‘’으로 사용한다. |
| \[def\_name\] | 추적하고자 하는 대상이다. |
| args\_indexes | 추적하고자 하는 대상의 아규먼트 인덱스. 여러 개일 경우로 구분한다. |
| kwargs | 추적하고자 하는 대상의 키워드 명. 여러 개일 경우로 구분한다. |

transaction\_enabled

트랜잭션 추적 기능을 활성화 합니다. 트랜잭션 데이터는 Hitmap에서 확인 가능합니다. 단, enable이 false면 무시됩니다.counter\_enabled

성능 카운터 추적 기능을 활성화합니다. 액티브트랜잭션 수, 사용자 수, JVM 자원 사용량, Process CPU 사용량 및 DB Pool 사용량 정보등이 해당됩니다.

* Default : \[**true**\]
* Type : Boolean

stat\_enabled

통계정보 추적 기능을 활성화합니다. 5 분단위로 수집되는 트랜잭션, SQL, HTTPCALL, UserAgent, Client IP 등의 통계 데이터등이 해당됩니다.

* Default : \[**true**\]
* Type : Boolean

active\_stack\_enabled 액티브 스택 추적을 활성화 합니다. 참고로, counter\_enabled 값이 비활성화 된 경우 액티브 트랜잭션 데이터가 수집되지 않으므로 액티브 스택 또한 수집되지 않습니다.

TODO: 지원 예정입니다.

* Default : \[**true**\]
* Type : Boolean

### 보안 설정에 관한 설정 {#user-content-보안-설정에-관한-설정}

cypher\_level

TODO: 지원 예정입니다.

AES보안 알고리즘에 대한 암호 레벨을 지정합니다. \(값은 128, 256중 하나를 사용할 수 있습니다.\)

* Default : \[**128**\]
* Type : aes\_bit \[128\|256\]

encrypt\_level

TODO: 지원 예정입니다.

와탭 에이전트는 서버로 데이터 전송시 데이터 속성에 따라 선택적으로 암호화를 하므로 높은 보안을 유지하면서도 성능상 이점을 가지고 있습니다. 이와 별개로 데이터 유형에 상관없이 일괄적인 암호화 정책을 적용하려는 경우 당 옵션을 사용할 수 있습니다.

| Note | 1 - 암호화 전송 기능 사용안함 2 - SQL파라미터, Plain Text와 같은 민감한 속성에 대하여 암호화 전송 3 - 모든 항목에 대하여 암호화 전송 |
| :--- | :--- |


* Default : \[**2**\]
* Type : encrypt\_level \[1\|2\|3\]

### 트랜잭션 프로파일 데이터에 관한 설정 {#user-content-트랜잭션-프로파일-데이터에-관한-설정}

profile\_http\_header\_enabled

TODO: 지원 예정입니다.

프로파일 내역에 http 헤더 정보를 기록하고자 할 때 사용합니다.

* Default : \[**false**\]
* Type : Boolean

profile\_httpheader\_urlprefix

TODO: 지원 예정입니다.

프로파일 내역에 http 헤더 정보를 기록할 대상 URL의 prefix를 정의 할 때 사용합니다.

* Default : \[**/**\]
* Type : String

profile\_http\_parameter\_enabled

TODO: 지원 예정입니다.

프로파일 내역에 http 파라미터 정보를 기록하고자 할 때 사용합니다. 파라미터는 별도 보안키를 입력해야 조회 할 수 있습니다.

| Note | 보안 키는 WAS서버 ${WHATAP\_AGENT\_HOME}/paramkey.txt 파일내에 6자리로 지정합니다. paramkey.txt 파일이 존재하지 않는 경우 랜덤 값으로 자동 생성됩니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

profile\_http\_parameter\_urlprefix

TODO: 지원 예정입니다.

프로파일 내역에 http 파라미터 정보를 기록할 대상 URL의 prefix를 정의 할 때 사용합니다.

* Default : \[**/**\]
* Type : String

profile\_connection\_open\_enabled

프로파일 내역에 DBConnection 오픈 정보를 기록합니다.

* Default : \[**true**\]
* Type : Boolean

profile\_dbc\_close\(\*\)

profile\_connection\_open\_enabled이 활성화 되어 있는 경우, 프로파일에 DB Connection이 close될 때의 정보를 출력합니다.

* Default : \[**false**\]
* Type : Boolean \(profile\_connection\_open\_enabled=true 에서만 동작\)

profile\_step\_normal\_count

트랜잭션 프로파일의 최대 스텝 수를 지정합니다.

* Default: \[**1000**\]
* Type : Int

profile\_step\_heavy\_count

Heavy한 스텝의 경우 프로파일 기본 스텝 수를 초과하더라도 정해진 값 만큼은 기록 됩니다.

* Default: \[**1020**\]
* Type : Int

profile\_step\_max\_count

프로파일 스텝의 최대 수를 설정합니다. 수집된 프로파일 스텝 수가 이 값을 초과하면 이후 수집되는 스텝들은 모두 버려집니다. profile\_step\_heavy\_count을 최대 1000으로 설정한다면 profile\_step\_max\_count만큼 액티브 스택이 수집됩니다.

* Default: \[**1024**\]
* Type : Int

profile\_step\_heavy\_time

Heavy한 스텝의 기준을 지정 합니다. 지정된 값보다 수행시간이 긴 경우 profile\_step\_normal\_count 를 초과하는 경우라도 profile\_step\_heavy\_count 이내에서 기록됩니다.

* Default: \[**100**\]
* Type : MiliSecond

profile\_basetime

트랜잭션이 설정된 값 이하의 시간내에 종료된 경우 프로파일 정보를 수집하지 않습니다. 단, 5 분단위로 최초 호출된 URL, 에러가 발생한 트랜잭션에 대한 프로파일 정보는 수집됩니다.

* Default: \[**0**\]
* Type : MiliSecond

query\_string\_enabled

트랜잭션 URL의 쿼리 스트링을 함께 수집하는 기능을 활성화합니다.

* Default : \[**false**\]
* Type : Boolean

query\_string\_urls

트랜잭션에서 쿼리 스트링을 수집 할 URL들을 등록합니다. 여러 개를 등록할 때는 콤마\(,\)를 사용합니다.

* Default : \[**NONE**\]
* Type : String

6.5.8.14. profile\_sql\_param\_enabled TODO: 지원 예정입니다.

프로파일 내역에 SQL 파라미터 정보를 기록하고자 할 때 사용합니다. 파라미터는 별도 보안키를 입력해야 조회 할 수 있습니다.

| Note | 보안 키는 WAS서버 ${WHATAP\_AGENT\_HOME}/paramkey.txt 파일내에 6자리로 지정합니다. paramkey.txt 파일이 존재하지 않는 경우 랜덤 값으로 자동 생성됩니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

profile\_sql\_resource\_enabled

프로파일에서 SQL 이 수집될 때 해당 스텝에서 사용한 CPU 와 메모리 사용량을 추적합니다.

* Default : \[**false**\]
* Type : Boolean

profile\_method\_resource\_enabled

TODO: 지원 예정입니다.

프로파일에서 method 스텝이 수집될 때 해당 스텝에서 사용한 CPU 와 메모리 사용량을 추적합니다.

* Default : \[**false**\]
* Type : Boolean

profile\_httpc\_resource\_enabled

프로파일에서 HTTP Call 스텝이 수집될 때 해당 스텝에서 사용한 CPU 와 메모리 사용량을 추적합니다.

* Default : \[**false**\]
* Type : Boolean

profile\_position\_sql

TODO: 지원 예정입니다.

SQL이 수행되는 시점의 StackTrace를 기록한다.

* Default : \[**false**\]
* Type : Boolean

profile\_position\_httpc

TODO: 지원 예정입니다.

HTTPC가 수행되는 시점의 StackTrace를 기록합니다.

* Default : \[**false**\]
* Type : Boolean

profile\_position\_method

TODO: 지원 예정입니다.

지정한 메소드가 수행되는 시점의 StackTrace를 기록합니다.

* Default : \[**NONE**\]
* Type : String

profile\_position\_depth

TODO: 지원 예정입니다.

position 추적을 위해 StackTrace를 기록 할 때 최대 라인 수를 지정합니다.

* Default : \[**50**\]
* Type : Int

profile\_error\_sql\_fetch\_max

TODO: 지원 예정입니다.

SQL 수행후 Fetch Count 가 지정한 값을 초과하면 TOO MANY Fetch 에러로 처리됩니다.

* Default : \[**10000**\]
* Type : Int

profile\_error\_sql\_time\_max

TODO: 지원 예정입니다.

SQL 수행후 수행시간이 여기서 지정한 값을 초과하면 TOO SLOW 에러로 처리됩니다.

* Default : \[**30000**\]
* Type : MiliSecond

### 사용자 추적을 위한 설정 {#user-content-사용자-추적을-위한-설정}

trace\_user\_enabled\(\*\)

실시간 사용자를 추적할지를 결정합니다. 이 값을 활성화 하는 경우 기본값은 IP가 됩니다.

* Default : \[**true**\]
* Type : Boolean

trace\_user\_using\_ip\(\*\)

실시간 사용자의 구분을 IP로 하고자 하는 경우 설정합니다. 이 데이터는 Real Time User에서 확인 가능합니다. 단, user\_header\_ticket옵션과 배타적으로 설정을 동시에 적용할 수 없습니다.

* Default : \[**true**\]
* Type : Boolean

trace\_user\_header\_ticket

TODO: 지원 예정입니다.

사용자의 구분을 HTTP 헤더의 특정 값으로 구분하고 싶을 때 사용 할 HTTP 키를 지정합니다. 단, trace\_user\_using\_ip 배타적으로 설정을 동시에 적용할 수 없습니다.

* Default : \[**NONE**\]
* Type : String

trace\_user\_cookie\_limit

TODO: 지원 예정입니다.

사용자 집계를 위해 쿠키를 발행하는 경우 기존 쿠키가 너무 많다면 쿠키 오버플로어가 발생 할 수 있습니다. 이를 회피하기 위해 limit 를 지정합니다.

* Default: \[**2048**\]
* Type : Int

trace\_http\_client\_ip\_header\_key

TODO: 지원 예정입니다.

Remote Address 를 http header의 특정 key값으로 대체합니다.

| Note | WEB/WAS 앞에 L4와 같은 로드밸런서가 위치한 경우 Client의 IP가 아닌 L4의 IP가 Remote Address가 되는 경우가 있습니다. 이 상황에서 실제 Client IP정보가 http header에 특정 key 값으로 기록되는 경우라면 해당 key로 대체 할 수 있습니다. |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String
* Ex : trace\_http\_client\_ip\_header\_key=x-fowarded-for

### 백그라운드 트랜잭션 추적을 위한 설정 {#user-content-백그라운드-트랜잭션-추적을-위한-설정}

trace\_auto\_transaction\_enabled

TODO: 지원 예정입니다.

백그라운드 호출을 하나의 트랜잭션으로 수집하여 데이터를 추적하고 싶을 때, 트랜잭션의 END POINT를 설정 할 수 있습니다. 프로덕션 보다는 주로 개발 환경에서 사용합니다.

| Note | 주로 개발환경에서 백그라운드 트랜잭션의 END POINT 를 찾아낼 때 사용합니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

trace\_auto\_transaction\_backstack\_enabled

TODO: 지원 예정입니다.

trace\_auto\_transaction\_enabled=true 이 설정된 경우에 트랜잭션 시작시 StackTrace를 기록합니다. 이를 통해 트랜잭션의 시작점을 찾아낼 수 있습니다.

* Default : \[**true**\]
* Type : Boolean

trace\_background\_socket\_enabled

TODO: 지원 예정입니다.

트랜잭션이 아닌 백그라운드 쓰레드에 의한 소켓이 오픈될 때도 이를 기록합니다.

* Default : \[**true**\]
* Type : Boolean

### 트랜잭션 추적을 위한 설정 {#user-content-트랜잭션-추적을-위한-설정}

trace\_transaction\_name\_header\_key

TODO: 지원 예정입니다.

설정 된 HTTP 헤더의 키 값을 트랜잭션 URL에 추가합니다. 동일한 URL에서 HTTP 헤더의 키를 구분하여 트랜잭션을 세밀하게 나누어 데이터추적이 가능합니다.

* Default : \[**NONE**\]
* Type : String

trace\_transaction\_name\_key

TODO: 지원 예정입니다.

설정 된 HTTP 요청 파라미터의 값을 트랜잭션 URL에 추가합니다. 동일한 URL에서 파라미터를 구분하여 트랜잭션을 세밀하게 나누어 데이터추적이 가능합니다.

* Default : \[**NONE**\]
* Type : String

trace\_error\_callstack\_depth

트랜잭션에서 에러 콜 스택을 수집할 때, 콜스택 최대 라인수를 지정합니다. 이 데이터는 에러 통계데이터에서 조회 할 수 있습니다.

* Default: \[**50**\]
* Type : Int

trace\_active\_callstack\_depth

트랜잭션에서 액티브 스택을 수집할 때, 콜스택 최대 라인수를 지정합니다.

* Default: \[**50**\]
* Type : Int

trace\_active\_transaction\_slow\_time

엑티브 트랜잭션의 아크이퀄라이저에서 slow 구간의 응답기준을 지정합니다.

* Default: \[**3000**\]
* Type : MiliSecond

trace\_active\_transaction\_very\_slow\_time

엑티브 트랜잭션의 아크이퀄라이저에서 very slow 구간의 응답기준을 지정합니다.

* Default: \[**8000**\]
* Type : MiliSecond

trace\_active\_transaction\_lost\_time

트랜잭션의 종료를 기다리는 제한 시간. 5분안에 트랜잭션이 끝나지 않는 경우 트랜잭션을 정보를 더이상 수집하지 않습니다.

* Default: \[**300000**\]
* Type : MiliSecond

trace\_dbc\_leak\_enabled

TODO: 지원 예정입니다.

DB Connection Leak을 추적하는 기능을 활성화 합니다.

* Default : \[**false**\]
* Type : Boolean

trace\_dbc\_leak\_fullstack\_enabled

DBConnection Leak이 감지되는 경우 해당 시점 StackTrace를 수집합니다.

| Warning | 옵션 적용시 CPU 사용량이 다소 증가할 수 있습니다. PeakTime시 적용을 피하고 문제해결 용도로만 한시적으로 적용 할 것을 권고합니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

6.5.11.10. debug\_dbc\_stack\_enabled TODO: 지원 예정입니다.

DB Connection 시점의 StackTrace 를 프로파일에 저장합니다. 어플리케이션에서 사용하는 Connection Pool 정보를 얻기위해 사용됩니다.

* Default : \[**false**\]
* Type : Boolean

trace\_gtx\_rate

TODO: 지원 예정입니다.

와탭 에이전트가 등록된 애플리케이션 들의 관계를 확인 하기 위해 발급되는 gtx에 대해, 관계를 파악하기 위한 용도로 사용될 gtx사용율.

* Default : \[**0**\]
* Type : Percentage

web\_static\_content\_extensions\(\*\)

스태틱 컨텐츠임을 판단하는 확장자를 지정합니다. 여기에 설정된 확장자를 가진 트랜잭션들은 프로파일 추적과 카운팅이 제외됩니다.

* Default : \[**js, htm, html, gif, png, jpg, css, swf, ico**\]
* Type : String

### 운영을 위한 설정 {#user-content-운영을-위한-설정}

active\_stack\_second

액티브 스택을 추적하는 간격을 설정합니다. \(주의: 값을 바꾸는 것을 권장하지 않습니다.\)

| Warning | 값을 바꾸는 것을 권장하지 않습니다. |
| :--- | :--- |


* Default : \[**10**\]
* Type : Seconds

counter\_procfd\_enabled

TODO: 지원 예정입니다.

파일 디스크립터 수를 추적하는 기능을 활성화합니다.

* Default : \[**false**\]
* Type : Boolean

counter\_netstat\_enabled

TODO: 지원 예정입니다.

NET STAT 상태별 건수를 모니터링합니다. ESTABLISH, CLOSE\_WAIT, FIN\_WAIT 등 상태별 건수를 수집합니다.

* Default : \[**false**\]
* Type : Boolean

realtime\_user\_thinktime\_max

실시간 사용자 측정시 동일 사용자로 인정되는 최대 호출간격을 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds

time\_sync\_interval\_ms

에이전트와 서버간 시간 동기화 주기를 지정합니다. 동기화 하지 않을 경우 0으로 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds

detect\_deadlock\_enabled

TODO: 지원 예정입니다.

쓰레드 DeadLock 여부를 체크하여 감지시 이벤트를 발생시킵니다. 발생 주기는 5초 단위이며 같은 DeadLock 건에 대한 이벤트는 한시간에 한번만 발생시킵니다.

* Default : \[**false**\]
* Type : Boolean

text\_reset

와탭 에이전트는 한번 보낸 텍스트유형 데이터는 hash 처리되므로 다음날까지 재전송하지 않습니다. 이전 설정값과 다른 값을 설정하는 경우 재전송 합니다.

| Note | 트랜잭션 URL, SQL String 등이 텍스트유형 데이터에 해당합니다. |
| :--- | :--- |


* Default : \[**0**\]
* Type : Int

trace\_auto\_normalize\_enabled\(\*\)

트랜잭션 URL 정규화할때 패턴값을 어노테이션에서 추출하여 자동으로 파싱하는 기능을 활성화합니다.

* Default : \[**true**\]
* Type : Boolean

trace\_normalize\_enabled

트랜잭션 URL 을 파싱하여 정규화하는 기능을 활성화합니다.

| Note | false 로 변경시 패스파라미터 파싱이 비활성화됩니다. 이 경우 통계데이터의 의미가 약화됨으로 디버그 용도로만 잠시 사용하는 것이 좋습니다. |
| :--- | :--- |


* Default : \[**true**\]
* Type : Boolean

trace\_normalize\_urls

트랜잭션 URL을 파싱하여 정규화 합니다. 호출 URL패턴을 파싱하여 패스 파라미터를 제거합니다. 예를 들어, /a/{v}/b라고 선언하면 /a/123/b → /a/{v}/b로 치환합니다. 여러 개를 등록 할 때는 콤마\(,\)를 사용합니다. /a/\*/b 로 사용하여 특정 형식의 패스 파라미터를 제거하여 수집할 수 있습니다.

* Default : \[**NONE**\]
* Type : String

trace\_httpc\_normalize\_enabled

외부 HTTP 호출\(HTTP Call\) URL을 파싱하여 정규화 하는 기능을 활성화합니다.

* Default : \[**true**\]
* Type : Boolean

trace\_httpc\_normalize\_urls

외부 HTTP 호출하는 URL을 파싱하여 정규화합니다. 호출 URL패턴을 파싱하여 패스 파라미터를 제거합니다. 예를 들면, /a/{v}/b라고 선언하면 /a/123/b → /a/{v}/b로 치환한다. 여러 개를 등록 할 때는 콤마\(,\)를 사용합니다. /a/\*/b 로 사용하여 특정 형식의 패스 파라미터를 제거하여 수집할 수 있습니다.

* Default : \[**NONE**\]
* Type : String

trace\_sql\_normalize\_enabled

SQL문에서 리터럴 부분을 추출하여 SQL문을 정규화 하는 기능을 활성화합니다.

* Default : \[**true**\]
* Type : Boolean

### 로그를 위한 설정 {#user-content-로그를-위한-설정}

log\_rotation\_enabled

에이전트 로그파일을 매일 변경합니다. \(로그파일 기본 경로: $WHATAP\_HOME/logs/whatap-xxx.log\)

* Default : \[**true**\]
* Type : Boolean

log\_keep\_days

로그파일 보관기간을 설정합니다.

* Default : \[**7**\]
* Type : Day

## 인프라 모니터링 \(준비 중\) {#user-content-인프라-모니터링-준비-중}

### 확장팩 모니터링 {#user-content-확장팩-모니터링}

## 데이터베이스 모니터링 \(준비 중\) {#user-content-데이터베이스-모니터링-준비-중}
