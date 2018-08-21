# 설정 가이드

## Java 애플리케이션 모니터링 {#user-content-java-애플리케이션-모니터링}

### 에이전트 관리 {#user-content-에이전트-관리}

**에이전트 네이밍**

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

**에이전트 기능제어**

shutdown

true 인 경우 에이전트의 모든 동작을 중지하고 서버와의 연결을 종료합니다.

* Default : \[**false**\]
* Type : Boolean

enabled

전체 기능을 활성화 합니다. false인 경우에도 서버와 최소한의 통신을 유지하기 위한 정보는 전송됩니다.

* Default : \[**true**\]
* Type : Boolean

transaction\_enabled

트랜잭션 추적 기능을 활성화 합니다. Hitmap에 기록되는 트랜잭션 정보가 해당합니다.

* Default : \[**true**\]
* Type : Boolean \(enabled=false 인 경우 false\)

counter\_enabled

성능 카운터 추적 기능을 활성화합니다. 액티브트랜잭션 수, 사용자 수, JVM 자원 사용량, Process CPU 사용량 및 DB Pool 사용량 정보등이 해당됩니다.

* Default : \[**true**\]
* Type : Boolean \(enabled=false 인 경우 false\)

stat\_enabled

통계정보 추적 기능을 활성화합니다. 5 분단위로 수집되는 트랜잭션, SQL, HTTPCALL, UserAgent, Client IP 등의 통계 데이터등이 해당됩니다.

* Default : \[**true**\]
* Type : Boolean \(enabled=false 인 경우 false\)

sigar\_enabled

sigar library 를 통한 OS 정보 수집을 활성화합니다. 5 초 단위로 sigar library를 통해 수집되는 CPU, Memory, Disk등의 OS 자원 데이터가 해당됩니다.

* Default : \[**true**\]
* Type : Boolean \(enabled=false 인 경우 false\)

active\_stack\_enabled

액티브 스택 추적을 활성화합니다. 스텍 메뉴의 탑스택, 유니크스택 그리고 액티브스택이 해당됩니다.

* Default : \[**true**\]
* Type : Boolean \(enabled=false 또는 counter\_enabled=false 인 경우 false\)

license

에이전트 설치시 서버로부터 부여받은 라이센스를 지정합니다. 라이센스에는 에이전트가 속한 프로젝트와 보안 통신을 위한 암호키를 포함하고 있습니다.

* Default : \[**NONE**\]
* Type : String

cypher\_level

AES 보안 알고리즘에 대한 암호 레벨을 지정합니다.

* Default : \[**128**\]
* Type : aes\_bit \[128\|256\]

encrypt\_level

와탭 에이전트는 서버로 데이터 전송시 데이터 속성에 따라 선택적으로 암호화를 하므로 높은 보안을 유지하면서도 성능상 이점을 가지고 있습니다. 이와 별개로 데이터 유형에 상관없이 일괄적인 암호화 정책을 적용하려는 경우 당 옵션을 사용할 수 있습니다.

| Note | 1 - 암호화 전송 기능 사용안함 2 - SQL파라미터, Plain Text와 같은 민감한 속성에 대하여 암호화 전송 3 - 모든 항목에 대하여 암호화 전송 |
| :--- | :--- |


* Default : \[**2**\]
* Type : encrypt\_level \[1\|2\|3\]

stat\_ip\_enabled

"통계 \| 클라이언트IP" 항목의 IP 통계 사용 여부를 활성화합니다.

* Default : \[**true**\]
* Type : Boolean

realtime\_user\_enabled

"대시보드" 사용자 항목에서 사용되는 실시간 사용자 지표 수집 여부를 선택한다.

* Default : \[**true**\]
* Type : Boolean

hook\_direct\_patch\_classes

직접적으로 특정 클래스를 로딩타임에 바꿔치기 하고자 할 때 사용합니다. 클래스를 컴파일한 후에 별도 파일로 만들고 그 파일의 풀패스를 지정합니다.

* Default : \[**NONE**\]
* Type : ClassFile\_FullPath

active\_stack\_second

액티브 스택을 추적하는 간격을 지정합니다.

| Warning | 값을 바꾸는 것을 권장하지 않습니다. |
| :--- | :--- |


* Default : \[**10**\]
* Type : Seconds

boot\_redefine\_size

Attach 방식이나 Watcher 방식으로 설치했을 때 이미 로딩된 클래스 중에 추적을 위해 BCI 를 새로 수행하게 됩니다. 이때 동시 redefine 하는 클래스 수를 정의합니다.

* Default : \[**100**\]
* Type : Int

trace\_component\_enabled

서버 \| 더보기 \| 컴포넌트 버전 기능을 활성화 합니다.

* Default : \[**true**\]
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

Java 쓰레드의 DeadLock 여부를 체크하여 감지시 이벤트를 발생시킵니다. 발생 주기는 5초 단위이며 같은 DeadLock 건에 대한 이벤트는 한시간에 한번만 발생시킵니다.

* Default : \[**false**\]
* Type : Boolean

text\_reset

와탭 에이전트는 한번 보낸 텍스트유형 데이터는 hash 처리되므로 다음날까지 재전송하지 않습니다. 이전 설정값과 다른 값을 설정하는 경우 재전송 합니다.

| Note | 트랜잭션 URL, SQL String 등이 텍스트유형 데이터에 해당합니다. |
| :--- | :--- |


* Default : \[**0**\]
* Type : Int

**에이전트 통신**

whatap\_server\_host

에이전트가 수집한 데이터를 전송할 서버를 지정합니다. 수집서버 이중화로 2개 이상의 IP를 가진 경우 콤마\(,\)로 분리하여 지정할 수 있습니다. 지정된 IP 에는 수집서버 proxy 데몬이 리스닝 상태로 서비스 되어야 합니다.

* Default : \[**127.0.0.1,127.0.0.1**\]
* Type : ip\_address

whatap\_server\_port

수집서버 PORT 를 지정합니다. 포트는 하나만 지정할 수 있으므로 whatap\_server\_host 에 지정된 수집서버들은 동일 PORT 를 사용해야 합니다.

* Default : \[**6600**\]
* Type : tcp\_port

tcp\_so\_timeout

수집서버와 통신하는 TCP세션의 Socket Timeout 값을 지정합니다.

* Default : \[**60000**\]
* Type : MiliSecond

tcp\_connection\_timeout

수집서버와 통신하는 TCP세션의 Connection Timeout 값을 지정합니다.

* Default : \[**5000**\]
* Type : MiliSecond

net\_send\_max\_bytes

수집서버로 데이터를 전송할 때 한번에 전송되는 최대 크기를 지정합니다.

* Default : \[**5242880**\]
* Type : Byte

net\_send\_queue1\_size

프로파일 정보와 액티브스택을 제외한 나머지 데이터 전송에 사용될 Queue의 크기를 지정 합니다. 설정된 크기가 10 이하인 경우 10으로 지정됩니다.

* Default : \[**256**\]
* Type : Int

net\_send\_queue2\_size

프로파일 정보와 액티브스택 데이터 전송에 사용될 Queue의 크기를 지정 합니다. 설정된 크기가 10 이하인 경우 10으로 지정됩니다.

* Default : \[**512**\]
* Type : Int

**에이전트 로그 관리**

log\_datasource\_lookup\_enabled

InitialContext Lookup 시 DataSource 인 경우 로그를 기록하는 기능을 활성화 합니다.

* Default : \[**true**\]
* Type : Boolean

log\_rotation\_enabled

에이전트 로그파일을 일자별로 관리하는 기능을 활성화 합니다.

* Default : \[**true**\]
* Type : Boolean

log\_keep\_days

로그파일 보관기간을 지정합니다.

* Default : \[**7**\]
* Type : Day

### 트랜잭션 프로파일링 {#user-content-트랜잭션-프로파일링}

profile\_step\_normal\_count

트랜잭션 프로파일의 최대 스텝 수를 지정합니다.

* Default: \[**1000**\]
* Type : Int

profile\_step\_heavy\_count

Heavy한 스텝의 경우 프로파일 기본 스텝 수를 초과하더라도 정해진 값 만큼은 기록 됩니다.

* Default: \[**1020**\]
* Type : Int

profile\_step\_heavy\_time

Heavy한 스텝의 기준을 지정 합니다. 지정된 값보다 수행시간이 긴 경우 profile\_step\_normal\_count 를 초과하는 경우라도 profile\_step\_heavy\_count 이내에서 기록됩니다.

* Default: \[**100**\]
* Type : MiliSecond

profile\_basetime

트랜잭션이 설정된 값 이하의 시간내에 종료된 경우 프로파일 정보를 수집하지 않습니다. 단, 5 분단위로 최초 호출된 URL, 에러가 발생한 트랜잭션에 대한 프로파일 정보는 수집됩니다.

* Default: 500
* Type : MiliSecond

active\_stack\_count

트랜잭션 내에서 수집하는 AtiveStack 의 최대 수를 지정합니다.

* Default : \[**100**\]
* Type : Int

profile\_method\_resource\_enabled

프로파일에서 method 스텝이 수집될 때 해당 스텝에서 사용한 CPU 와 메모리 사용량을 추적합니다.

* Default : \[**false**\]
* Type : Boolean

profile\_position\_method

지정한 메소드가 수행되는 시점의 StackTrace를 기록합니다.

* Default : \[**NONE**\]
* Type : String

profile\_position\_depth

position 추적을 위해 StackTrace를 기록 할 때 최대 라인 수를 지정합니다.

* Default : \[**50**\]
* Type : Int

trace\_error\_callstack\_depth

Error발생시 수집하는 StackTrace의 최대 라인 수를 지정합니다.

* Default: \[**50**\]
* Type : Int

trace\_active\_callstack\_depth

액티브스택에서 수집하는 StackTrace의 최대 라인수를 지정합니다

* Default: \[**50**\]
* Type : Int

trace\_active\_transaction\_yellow\_time

액티브 트랜잭션의 아크이퀄라이저에서 노란색으로 표현할 기준을 지정 합니다.

* Default: \[**3000**\]
* Type : MiliSecond

trace\_active\_transaction\_red\_time

액티브 트랜잭션의 아크이퀄라이저에서 빨간색으로 표현할 기준을 지정 합니다.

* Default: \[**8000**\]
* Type : MiliSecond

hook\_method\_patterns

응답시간을 측정할 메소드를 지정합니다. 마지막 \(.\)을 구분자로 클래스 FullName과 메소드로 구분되며 \(\*\)로 WildCard를 사용 할 수 있습니다. 대상이 여러개인 경우 콤마\(,\)로 구분합니다

* Default : \[**NONE**\]
* Type : String
* Ex : hook\_method\_patterns=a.b.C1.\*

hook\_method\_supers

특정 클래스를 상속받은 메소드의 응답시간을 측정하고자 할 때 Super Class를 지정합니다. 클래스 FullName을 지정하며 대상이 여러개인 경우 콤마\(,\)로 구분합니다.

* Default : \[**NONE**\]
* Type : String
* Ex : hook\_method\_supers=a.b.C1

hook\_method\_interfaces

특정 인터페이스를 구현한 메소드의 응답시간을 측정하고자 할 때 Interface를 지정합니다. 인터페이스 FullName을 지정하며 대상이 여러개인 경우 콤마\(,\)로 구분합니다.

* Default : \[**NONE**\]
* Type : String

hook\_method\_ignore\_prefixes

메소드 프로파일을 설정할 때 지정한 문자열로 시작하는 메소드들은 추적하지 않습니다. \* Default : \[**get,set** \]\* Type : Stringhook\_method\_ignore\_classes

메소드 프로파일을 설정할 때 프로파일에서 제외 하고 싶은 클래스들을 지정합니다.

* Default : \[**NONE**\]
* Type : String

hook\_method\_access\_public\_enabled

메소드 프로파일을 설정할 때 public 메소드에 대해서만 별도로 대상으로 할지를 결정합니다.

* Default : \[**true**\]
* Type : Boolean

hook\_method\_access\_private\_enabled

메소드 프로파일을 설정할 때 private 메소드에 대해서만 별도로 대상으로 할지를 결정합니다.

* Default : \[**false**\]
* Type : Boolean

hook\_method\_access\_protected\_enabled

메소드 프로파일을 설정할 때 protected 메소드에 대해서만 별도로 대상으로할지를 결정합니다.

* Default : \[**true**\]
* Type : Boolean

hook\_method\_access\_none\_enabled

메소드 프로파일을 설정할 때 no access indicated 메소드에 대해서만 별도로 대상으로 할지를 결정합니다.

* Default : \[**true**\]
* Type : Boolean

stacklog\_socket\_port

목적지의 TCP포트를 지정하면 Socket.connect\(\) 시점 StackTrace를 에이전트 로그로 기록합니다. 기본설정으로 확인되지 않는 DB 연결, HTTPC 연결등을 추적할 때 사용할 수 있습니다.

| Warning | 설정된 목적지로 연결시마다 매번 StackTrace를 기록하므로 성능저하를 유발할 수 있습니다. 디버깅 용도로 선별된 에이전트에 한시적으로만 사용해야 합니다. |
| :--- | :--- |


* Default : \[**0**\]
* Type : TCP\_PortNumber
* Ex : stacklog\_socket\_port=1521 \#DB연결 상태 추적

**HTTP**

profile\_http\_header\_enabled

프로파일 내역에 http 헤더 정보를 기록하고자 할 때 사용합니다.

* Default : \[**false**\]
* Type : Boolean

profile\_http\_header\_url\_prefix

프로파일 내역에 http 헤더 정보를 기록할 대상 URL의 prefix를 정의 할 때 사용합니다.

* Default : \[**/**\]
* Type : String

profile\_http\_parameter\_enabled

프로파일 내역에 http 파라미터 정보를 기록하고자 할 때 사용합니다. 파라미터는 별도 보안키를 입력해야 조회 할 수 있습니다.

| Note | 보안 키는 WAS서버 ${WHATAP\_AGENT\_HOME}/paramkey.txt 파일내에 6자리로 지정합니다. paramkey.txt 파일이 존재하지 않는 경우 랜덤 값으로 자동 생성됩니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

profile\_http\_parameter\_url\_prefix

프로파일 내역에 http 파라미터 정보를 기록할 대상 URL의 prefix를 정의 할 때 사용합니다.

* Default : \[**/**\]
* Type : String

trace\_transaction\_name\_header\_key

트랜잭션의 이름 끝부분에 지정한 http header key에서 추출한 값을 추가합니다.

* Default : \[**NONE**\]
* Type : String

trace\_transaction\_name\_key

트랜잭션의 이름 끝부분에 지정한 http request parameter 에서 추출한 값을 추가합니다.

* Default : \[**NONE**\]
* Type : String

trace\_normalize\_enabled

트랜잭션 URL 을 파싱하여 정규화하는 기능을 활성화합니다.

| Note | false 로 변경시 패스파라미터 파싱이 비활성화됩니다. 이 경우 통계데이터의 의미가 약화됨으로 디버그 용도로만 잠시 사용하는 것이 좋습니다. |
| :--- | :--- |


* Default : \[**true**\]
* Type : Boolean

trace\_auto\_normalize\_enabled

트랜잭션 URL 정규화할때 패턴값을 어노테이션에서 추출하여 자동으로 파싱하는 기능을 활성화합니다.

* Default : \[**true**\]
* Type : Boolean

trace\_normalize\_urls

정규화 할 트랜잭션 URL 패턴을 정의 한다. 호출 URL 패턴을 파싱하여 패스파라미터를 제거합니다.

| Note | ex\) /a/{v}/b 라고 선언하면 a/123/b ⇒ a/{v}/b 로 치환한다 여러 개를 등록할 때는 콤마\(,\)를 사용합니다. 치환패턴 정리 후 보완필요 |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String

web\_static\_content\_extensions

스태틱 컨텐츠임을 판단하는 확장자를 지정합니다. 여기에 설정된 확장자를 가진 트랜잭션들은 프로파일 추적과 카운팅이 제외됩니다.

* Default : \[**js, htm, html, gif, png, jpg, css, swf, ico**\]
* Type : String

recursive\_max

트랜잭션의 재귀호출 여부 검출을 위한 옵션으로, 단일 트랜잭션으로 부터 파생되는 재귀호출 횟수를 카운트하여 이벤트 알림을 발행하기 위한 기준을 지정합니다.

| Note | HTTP URL 재귀호출을 대상으로 함 jsp:forward 를 통해 재호출 되는 케이스도 카운트에 포함됨 |
| :--- | :--- |


* Default : \[**1000000**\]
* Type : Int

mtrace\_rate

MTID 를 추적하면 등록된 모든 애플리케이션간의 호출을 확인 할 수 있습니다. 최초 트랜잭션이 발생할 때 발급받는 MTID\(Multi Transaction ID\)의 발급비율을 설정하는 옵션이다. 같은 프로젝트에 속한 애플리케이션은 Caller & Callee 기능을 통해 트랜잭션의 프로파일을 바로 확인 가능합니다.

* Default : \[**0**\]
* Type : Percentage

mtrace\_caller\_key

MTID 추적에 사용할 Caller Key Name을 정합니다.

* Default : \[**x-wtap-mst**\]
* Type : String

mtrace\_callee\_key

MTID 추적에 사용할 Callee Key Name을 정합니다.

* Default : \[**x-wtap-tx**\]
* Type : String

hook\_httpservlet\_classes

HTTP 트랜잭션의 END POINT 를 추가로 지정한다. 메소드의 첫번째 2 개의 파라미터는 HttpServletRequest 와 HttpServletResponse 만 지정 가능합니다.

* Default : \[**NONE**\]
* Type : String

hook\_jsp\_patterns

JSP 파일을 로딩하는 메소드를 지정합니다. 트랜잭션 호출 결과로 반환되는 JSP 정보를 프로파일에 표시합니다. 본 옵션을 통해 추가한 설정에 default 설정이 자동으로 추가됩니다.

* Default : \[**org.apache.jasper.servlet.JspServlet.serviceJspFile**\]
* Type : String

trace\_ignore\_url\_set

트랜잭션 추적에서 제외할 URL을 지정한다.

* Default : \[**NONE**\]
* Type : String

trace\_ignore\_url\_prefix

트랜잭션 추적에서 제외할 URL prefix를 지정한다.

* Default : \[**NONE**\]
* Type : String

**NON-Http**

trace\_auto\_transaction\_enabled

프로파일 대상 메소드가 트랜잭션 시작점\(Javax.http.httpservlet, hook\_service\_\*\) 내에서 수행되는 경우가 아니라면 수집이 되지 않습니다. 이 경우 프로파일 대상 메소드가 트랜잭션 시작점이 되도록 지정합니다.

| Note | 주로 개발환경에서 백그라운드 트랜잭션의 END POINT 를 찾아낼 때 사용합니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

trace\_auto\_transaction\_backstack\_enabled

trace\_auto\_transaction\_enabled=true 이 설정된 경우에 트랜잭션 시작시 StackTrace를 기록합니다. 이를 통해 트랜잭션의 시작점을 찾아낼 수 있습니다.

* Default : \[**true**\]
* Type : Boolean

trace\_background\_socket\_enabled

트랜잭션이 아닌 백그라운드 쓰레드에 의한 소켓이 오픈될 때도 이를 기록합니다.

* Default : \[**true**\]
* Type : Boolean

async\_stack\_enabled

Async 트랜잭션에 대한 Active Stack 기능 사용 여부를 선택한다.

* Default : \[**false**\]
* Type : Boolean

hook\_service\_patterns

NON-Http 트랜잭션 추적을 위한 시작점 패턴을 설정한다.

* Default : \[**NONE**\]
* Type : String

hook\_service\_supers

NON-Http 트랜잭션 추적을 위한 시작점의 공통 분모가 특정 클래스의 메소드를 상속받은 경우라면 이를 설정한다.

* Default : \[**NONE**\]
* Type : String

hook\_service\_interfaces

NON-Http 트랜잭션 추적을 위한 시작점의 공통 분모가 특정 인터페이스를 구현한 경우라면 이를 설정한다.

* Default : \[**NONE**\]
* Type : String

hook\_service\_access\_public\_enabled

Non Http Demon 프로세스의 트랜잭션을 지정할 때 public 메소드에 대해서만 Access 권한을 기준으로 on/off 를 지정합니다

* Default : \[**true**\]
* Type : Boolean

hook\_service\_access\_private\_enabled

Non Http Demon 프로세스의 트랜잭션을 지정할 때 private 메소드에 대해서만 Access 권한을 기준으로 on/off 를 지정합니다

* Default : \[**true**\]
* Type : Boolean

hook\_service\_access\_protected\_enabled

Non Http Demon 프로세스의 트랜잭션을 지정할 때 protected 메소드에 대해서만 Access 권한을 기준으로 on/off 를 지정합니다

* Default : \[**true**\]
* Type : Boolean

hook\_future\_classes

java.util.concurrent.Future 인터페이스를 implement 한 클래스를 설정하여 비동기 클래스를 추적하고자 할 때 활용합니다. full package class 명을 컴마\(,\) 구분자를 사용하여 복수의 클래스를 지정할 수 있습니다.

* Default : \[**NONE**\]
* Type : String

hook\_future\_prefix

java.util.concurrent.Future 인터페이스를 implement 한 클래스를 설정하여 비동기 클래스를 추적하고자 할 때 활용합니다. full package class 명의 prefix 를 지정하며, 컴마\(,\) 구분자를 사용하여 복수의 prefix 를 지정할 수 있습니다.

* Default : \[**NONE**\]
* Type : String

hook\_runnable\_classes

java.lang.Runnable 인터페이스를 implement 한 클래스를 설정하여 비동기 클래스를 추적하고자 할 때 활용합니다. full package class 명을 컴마\(,\) 구분자를 사용하여 수의 클래스를 지정할 수 있습니다.

* Default : \[**NONE**\]
* Type : String

hook\_runnable\_prefix

java.lang.Runnable 인터페이스를 implement 한 클래스를 설정하여 비동기 클래스를 추적하고자 할 때 활용합니다. full package class 명의 prefix 를 지정하며, 컴마\(,\) 구분자를 사용하여 복수의 prefix 를 지정할 수 있습니다.

* Default : \[**NONE**\]
* Type : String

**DB, SQL**

dbcp\_pool\_enabled

JMX를 사용하지 않고 DBCP의 DB Connection 정보를 추적하기 위해 사용됩니다.

* Default : \[**true**\]
* Type : Boolean

hikari\_pool\_enabled

JMX를 사용하지 않고 hikari pool의 DB Connection 정보를 추적하기 위해 사용됩니다.

* Default : \[**false**\]
* Type : Boolean

tomcat\_ds\_enabled

JMX를 사용하여 Tomcat DB Connection Pool 정보를 추적하는 기능을 활성화 합니다.

* Default : \[**false**\]
* Type : Boolean

tomcat\_pool\_enabled

JMX를 사용하지 않고 Tomcat DB Connection Pool 정보를 추적하는 기능을 활성화 합니다.

* Default : \[**true**\]
* Type : Boolean

weblogic\_ds\_enabled

JMX를 사용하여 Weblogic DB Connection Pool 정보를 추적하는 기능을 활성화 합니다.

* Default : \[**false**\]
* Type : Boolean

weblogic\_pool\_enabled

JMX를 사용하지 않고 Weblogic DB Connection Pool 정보를 추적하는 기능을 활성화 합니다.

* Default : \[**true**\]
* Type : Boolean

jeus\_pool\_enabled

JMX를 사용하지 않고 JEUS DB Connection Pool 정보를 추적하는 기능을 활성화 합니다.

* Default : \[**true**\]
* Type : Boolean

profile\_connection\_open\_enabled

프로파일 내역에 DBConnection 오픈 정보를 기록합니다.

* Default : \[**true**\]
* Type : Boolean

profile\_dbc\_close

프로파일 내역에 DBConnection 클로즈 정보를 기록합니다.

* Default : \[**false**\]
* Type : Boolean \(profile\_connection\_open\_enabled=true 에서만 동작\)

profile\_sql\_param\_enabled

프로파일 내역에 SQL 파라미터 정보를 기록하고자 할 때 사용합니다. 파라미터는 별도 보안키를 입력해야 조회 할 수 있습니다.

| Note | 보안 키는 WAS서버 ${WHATAP\_AGENT\_HOME}/paramkey.txt 파일내에 6자리로 지정합니다. paramkey.txt 파일이 존재하지 않는 경우 랜덤 값으로 자동 생성됩니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

profile\_sql\_resource\_enabled

프로파일에서 SQL 이 수집될 때 해당 스텝에서 사용한 CPU 와 메모리 사용량을 추적합니다.

* Default : \[**false**\]
* Type : Boolean

profile\_update\_count

excuteUpdate\(\) 메소드를 통해 SQL UPDATE문이 수행된 경우 UPDATE 건수를 수집합니다.

* Default : \[**false**\]
* Type : Boolean

custom\_pool\_classes

pre-define되지 않는 별도의 Connection Pool을 사용하는 경우 해당 클래스 명을 지정한다.

* Default : \[**NONE**\]
* Type : String

ds\_update\_interval

DB Connection 정보 Count 주기를 설정한다.

* Default : \[**5000**\]
* Type : MiliSeconds

profile\_position\_sql

SQL이 수행되는 시점의 StackTrace를 기록한다.

* Default : \[**false**\]
* Type : Boolean

trace\_dbc\_leak\_enabled

DBConnection Leak 을 추적하는 기능을 활성화합니다.

| Warning | Connection Wrapper를 사용해 Leak을 추적하기에 운영 서비스에 영향을 미칠 수 있으므로 반드시 테스트후 적용해야 합니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

trace\_dbc\_leak\_fullstack\_enabled

DBConnection Leak이 감지되는 경우 해당 시점 StackTrace를 수집합니다.

| Warning | 옵션 적용시 CPU 사용량이 다소 증가할 수 있습니다. PeakTime시 적용을 피하고 문제해결 용도로만 한시적으로 적용 할 것을 권고합니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

trace\_sql\_normalize\_enabled

SQL 문에서 리터럴 부분을 축출하여 SQL 문을 정규화하는 기능을 활성화합니다.

* Default : \[**true**\]
* Type : Boolean

profile\_error\_jdbc\_fetch\_max

SQL 수행후 Fetch Count\(ResultSet.next\(\) 호출 건 수\)가 지정한 값을 초과하면 TOO MANY Fetch 에러로 처리됩니다.

* Default : \[**10000**\]
* Type : Int

profile\_error\_sql\_time\_max

SQL 수행후 수행시간이 여기서 지정한 값을 초과하면 TOO SLOW 에러로 처리됩니다.

* Default : \[**30000**\]
* Type : MiliSecond

hook\_connection\_open\_patterns

DB Connection Open 시 호출되는 메소드를 등록합니다. 미리 지정되지 않은 Connection Pool 의 getConnection을 등록하는 것이 일반적입니다.

* Default : \[**NONE**\]
* Type : String
* Ex : hook\_connection\_open\_patterns=mypool.ConPool.getConnection

hook\_jdbc\_con\_classes

미등록 되었던 JDBC Connection 클래스를 지정합니다. \* Default : \[**NONE**\] \* Type : String \* Ex : hook\_jdbc\_con\_classes=mypool.ConPoolhook\_jdbc\_pstmt\_classes

미등록 되었던 jdbc PreparedStatement 클래스를 지정합니다. 주의할 점은 생성자 파라미터에 SQL 문자열이 전달되는 구조여야 합니다.

* Default : \[**NONE**\]
* Type : String
* Ex : org.apache.derby.impl.jdbc.EmbedPreparedStatement

hook\_jdbc\_cstmt\_classes

미등록 되었던 jdbc CallableStatement 클래스를 지정합니다.

* Default : \[**NONE**\]
* Type : String
* Ex : org.apache.derby.impl.jdbc.EmbedCallableStatement

hook\_jdbc\_stmt\_classes

미등록 되었던 JDBC Statement 클래스를 지정합니다.

* Default : \[**NONE**\]
* Type : String
* Ex : org.apache.derby.impl.jdbc.EmbedStatement

hook\_jdbc\_rs\_classes

미등록되었던 JDBC ResultSet 클래스를 지정합니다.

* Default : \[**NONE**\]
* Type : String
* Ex : org.apache.derby.impl.jdbc.EmbedResultSet

hook\_jdbc\_wrapping\_driver\_patterns

DB2 드라이버처럼 난독 처리된 JDBC 드라이버는 hook\_jdbc\_xxx 옵션으로 직접 BCI 가 어렵다. 이런 경우 Wrapper 방식으로 SQL 추적할 수 있는데 이때 Driver.connect 를 지정하여 추적하게 됩니다.

* Default : \[**NONE**\]
* Type : String

debug\_dbc\_stack\_enabled

DB Connection 시점의 StackTrace 를 프로파일에 저장합니다. 어플리케이션에서 사용하는 Connection Pool 정보를 얻기위해 사용됩니다.

* Default : \[**false**\]
* Type : Boolean

**HTTPC, API Call**

profile\_httpc\_resource\_enabled

프로파일에서 HTTP Call 스텝이 수집될 때 해당 스텝에서 사용한 CPU 와 메모리 사용량을 추적합니다.

* Default : \[**false**\]
* Type : Boolean

profile\_position\_httpc

HTTPC가 수행되는 시점의 StackTrace를 기록합니다.

* Default : \[**false**\]
* Type : Boolean

trace\_httpc\_normalize\_enabled

트랜잭션내 HTTPC URL 을 파싱하여 정규화하는 기능을 활성화합니다.

* Default : \[**true**\]
* Type : Boolean

trace\_httpc\_normalize\_urls

정규화 할 HTTPC URL 패턴을 정의 한다. 호출 URL 패턴을 파싱하여 패스파라미터를 제거합니다.

| Note | ex\) /a/{v}/b 라고 선언하면 a/123/b ⇒ a/{v}/b 로 치환한다 여러 개를 등록할 때는 콤마\(,\)를 사용합니다. 치환패턴 정리 후 보완필요 |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String

hook\_httpc\_patterns

HTTP Call 을 수행하는 클래스를 지정합니다.

* Default : \[**NONE**\]
* Type : String

**Plugin**

hook\_trace\_helper\_patterns

메소드 실행 및 종료 부분에서 프로파일 플러그인을 삽입할 포인트\(클래스 및 메소드명\)를 지정합니다

| Note | plugin 을 활용한 커스터마이즈 된 profile 정보 수집을 위한 용도로 하기 plugin 코드가 주입됩니다. $WHATAP\_HOME/plugin/TraceHelperStart.x $WHATAP\_HOME/plugin/TraceHelperEnd.x |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String

hook\_trace\_helper\_end\_patterns

메소드 종료 부분에서 프로파일 플러그인을 삽입할 포인트\(클래스 및 메소드명\)를 지정합니다.

| Note | plugin 을 활용한 커스터마이즈 된 profile 정보 수집을 위한 용도로 하기 plugin 코드가 주입됩니다. $WHATAP\_HOME/plugin/TraceHelperEnd.x |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String

hook\_trace\_helper\_start\_patterns

메소드 시작 부분에서 프로파일 플러그인을 삽입할 포인트\(클래스 및 메소드명\)를 지정합니다.

| Note | plugin 을 활용한 커스터마이즈 된 profile 정보 수집을 위한 용도로 하기 plugin 코드가 주입됩니다. $WHATAP\_HOME/plugin/TraceHelperStart.x  |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String

### 사용자 수 {#user-content-사용자-수}

trace\_user\_enabled

실시간 사용자 집계 여부를 지정합니다.

| Note | 사용자 추적 옵션이 중복 설정 된 경우 동작 우선순위 1. trace\_user\_using\_ip 2. trace\_user\_using\_jsession 3. user\_header\_ticket |
| :--- | :--- |


* Default : \[**true**\]
* Type : Boolean

trace\_user\_cookie\_limit

사용자 집계를 위해 쿠키를 발행하는 경우 기존 쿠키가 너무 많다면 쿠키 오버플로어가 발생 할 수 있습니다. 이를 회피하기 위해 limit 를 지정합니다.

* Default: \[**2048**\]
* Type : Int

trace\_user\_using\_ip

실시간 사용자 집계시 IP 를 기반으로 합니다.

* Default : \[**true**\]
* Type : Boolean

trace\_user\_using\_jsession

실시간 사용자 집계시 SESSIONID 를 기반으로 합니다.

* Default : \[**false**\]
* Type : Boolean

trace\_http\_client\_ip\_header\_key

Remote Address 를 http header의 특정 key값으로 대체합니다.

| Note | WEB/WAS 앞에 L4와 같은 로드밸런서가 위치한 경우 Client의 IP가 아닌 L4의 IP가 Remote Address가 되는 경우가 있습니다. 이 상황에서 실제 Client IP정보가 http header에 특정 key 값으로 기록되는 경우라면 해당 key로 대체 할 수 있습니다. |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String
* Ex : trace\_http\_client\_ip\_header\_key=x-fowarded-for

user\_header\_ticket

HTTP Header 의 특정 값으로 사용자 수를 집계하고자 하는 경우 해당 Key값을 지정합니다.

* Default : \[**NONE**\]
* Type : String

### 부하량 제어 {#user-content-부하량-제어}

throttle\_enabled

어플리케이션의 최대 동시 처리 수를 제한하는 쓰로틀링 기능을 활성화합니다. throttle\_ 으로 시작하는 모든 옵션은 throttle\_enabled=true 상태에서만 동작합니다.

| Note | 쓰로틀링 제어와 관련한 정책은 다음과 같은 우선순위를 가지고 있습니다. 1. Block : URL, 사용자IP 기준으로 서비스를 차단하며 가장 우선하여 적용됩니다. 2. Passing : Passing에 적용된 URL들은 Reject 정책보다 우선합니다. 3. Reject : Block, Passing 정책 이후에 Reject 정책이 적용됩니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

throttle\_limit

에이전트별 동시 처리되는 요청\(트랜잭션\)수가 지정한 값을 넘으면 추가로 도달하는 요청은 reject됩니다.

* Default: \[**10000**\]
* Type : Int

throttle\_rejected\_message

쓰로틀링 제한시 사용자에게 전달될 메시지를 정의합니다.

* Default : \[**too many request!!**\]
* Type : String

throttle\_rejected\_forward

사용자 요청이 limit 값을 넘어 reject 될 때 사용자에게 전달되는 안내 페이지 URL을 정의합니다. throttle\_rejected\_message와 동시에 설정된 경우 throttle\_rejected\_forward 가 우선적용 됩니다.

| Caution | 안내페이지가 동일한 컨테이너에서 서비스 되는 경우, 이 역시 동시처리 수에 산정 되므로 제귀호출로 인한 장애요소가 될 수 있습니다. 그러므로 안내 페이지는 static html 페이지로 만들거나 외부에 있어야 합니다. |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : URL

reject\_event\_enabled

사용자 요청이 Reject된 경우 이벤트 알람을 발생할 지를 정의합니다.

* Default : \[**false**\]
* Type : Boolean

reject\_event\_interval

Reject에 대한 이벤트 알람 발생이후 설정된 시간동안 중복된 이벤트에 대하여 알람 발생을 하지 않습니다.

* Default: \[**30000**\]
* Type : MiliSecond

throttle\_blocking\_url

throttle\_limit을 초과하지 않는 경우라도 블럭킹\(처리 거부\) 할 URL 을 지정합니다. 시스템 장애를 유발하는 URL을 긴급하게 블럭킹 하기 위해 사용할 수 있습니다.

* Default: \[**NONE**\]
* Type : String

throttle\_blocking\_ip

사용자 IP를 기준으로 블럭킹하고자 할 때 지정합니다. 디도스 공격이나 잘못된 사용자를 IP 기반으로 차단 할 때 사용할 수 있습니다. 여러개인 경우 콤마\(,\)를 사용합니다.

* Default: \[**NONE**\]
* Type : ip\_address

throttle\_target\_urls

등록된 URL을 대상으로만 쓰로틀 기능을 적용한다. 여러개인 경우 콤마\(,\) 로 구분합니다.

* Default: \[**NONE**\]
* Type : URL

throttle\_passing\_url

throttle\_limit을 초과하는 경우라도 처리되어야 할 URL이 있는 경우 지정합니다. 여러개인 경우 콤마\(,\)를 사용합니다.

* Default: \[**NONE**\]
* Type : String

throttle\_passing\_url\_prefix

throttle\_limit을 초과하는 경우라도 처리되어야 할 URL들을 prefix로 경우 지정합니다. 여러개인 경우 콤마\(,\)를 사용합니다.

* Default: \[**NONE**\]
* Type : String

throttle\_blocked\_message

요청이 블러킹 된 사용자에게 전달할 메시지를 정의합니다.

* Default : \[**request blocked!!**\]
* Type : String

throttle\_blocked\_forward

요청이 블러킹 된 사용자에게 전달할 URL을 정의합니다. throttle\_blocked\_message와 동시에 설정된 경우 throttle\_blocked\_forward 가 우선적용 됩니다.

* Default : \[**NONE**\]
* Type : URL

### 알림 설정 {#user-content-알림-설정}

recursive\_max

HTTP URL에서 재귀적으로 forward 되는 요청에 대한 경고 알림 설정 트랜잭션의 재귀 호출 여부 검출을 위한 옵션으로, 단일 트랜잭션으로 부터 파생되는 재귀 호출 횟수를 카운트하여 이벤트 알림을 발행하기 위한 기준을 지정합니다.

| Note | jsp:forward 를 통해 재호출 되는 케이스도 카운트에 포함됩니다. |
| :--- | :--- |


* Default : = \[**1000000**\]

recursive\_event\_interval

트랜잭션의 재귀 호출에 대한 이벤트 알림 발행 간격을 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds

reject\_event\_enabled

서비스 거절\(호출 부하 제한/거절\)\)시 이벤트 알림 발행 여부를 지정합니다.

* Default : \[**false**\]
* Type : Boolean

reject\_event\_interval

서비스 거절\(호출 부하 제한/거절\)\)시 이벤트 알림 발행 간격을 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds

httpc\_event\_enabled

HTTPC 연결오류 발생시 이벤트 알림 발행 여부를 지정합니다.

* Default : \[**false**\]
* Type : Boolean

httpc\_event\_interval

HTTPC 연결오류 발생시 이벤트 알림 발행 간격을 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds

heap\_event\_enabled

힙 사용량 임계 도달 시 이벤트 알림 발행 여부를 지정합니다.

* Default : \[**false**\]
* Type : Boolean

heap\_event\_percent

힙사용량 이벤트 알림 발행 기준 임계치를 지정합니다.

* Default : \[**90**\]
* Type : Percentage

heap\_event\_duration

힙사용량 이벤트 알림 발행 기준 지속시간을 지정합니다.

* Default : \[**30000**\]
* Type : MiliSeconds

heap\_event\_interval

힙사용량 이벤트 알림 발행 간격을 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds

heap\_event\_action

힙사용량 이벤트 발생 시 실행할 동적 로딩 코드 지정

| Note | \($WHATAP\_HOME/plugin/ActionScript.x 에 작성한 Java 코드\)에 전달할 ID \($id 로 전달됨\) |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String

disk\_event\_enabled

디스크사용량 임계 도달 시 이벤트 알림 발행 여부를 지정합니다.

* Default : \[**false**\]
* Type : Boolean

disk\_event\_percent

디스크사용량 이벤트 알림 발행 기준 임계치를 지정합니다.

* Default : \[**90**\]
* Type : Percentage

disk\_event\_interval

디스크사용량 이벤트 알림 발행 간격을 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds

disk\_event\_action

디스크사용량 이벤트 발생 시 실행할 동적 로딩 코드 지정

| Note | \($WHATAP\_HOME/plugin/ActionScript.x 에 작성한 Java 코드\)에 전달할 ID \($id 로 전달됨\) |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String

cpu\_event\_enabled

CPU 사용량 임계 도달 시 이벤트 알림 발행 여부를 지정합니다.

* Default : \[**false**\]
* Type : Boolean

cpu\_event\_percent

CPU 사용량 이벤트 알림 발행 기준 임계치를 지정합니다.

* Default : \[**90**\]
* Type : Percentage

cpu\_event\_duration

CPU 사용량 이벤트 알림 발행 기준 지속시간을 지정합니다.

* Default : \[**30000**\]
* Type : MiliSeconds

cpu\_event\_interval

CPU 사용량 이벤트 알림 발행 간격을 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds

cpu\_event\_action

CPU 사용량 이벤트 발생 시, 실행할 동적 로딩 코드에 전달할 ID를 지정합니다.

| Note | \($WHATAP\_HOME/plugin/ActionScript.x 에 작성한 Java 코드\)에 전달할 ID \($id 로 전달됨\) |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String

dbc\_dup\_event\_enabled

DB Connection 이 중복 할당 되었을 때 이벤트 알림 발행여부를 지정합니다.

* Default : \[**false**\]
* Type : Boolean

dbc\_dup\_event\_fullstack\_enabled

DB Connection 이 중복 할당 될때 Stack 확보 여부를 지정합니다.

* Default : \[**false**\]
* Type : Boolean

exception\_event\_enabled

Exception 발생 시 이벤트 알림 발행 여부를 지정합니다.

* Default : \[**false**\]
* Type : Boolean

exception\_event\_interval

Exception 발생 시 이벤트 알림 발행 간격을 지정합니다.

* Default : \[**60000**\]
* Type : MiliSeconds

exception\_event\_set

대상 Exception 을 지정합니다. 여러개 지정할 경우 ','로 구분자를 사용합니다.

* Default : \[**Null**\]
* Type : String

exception\_event\_action

이벤트 발생 시 실행할 동적 로딩 코드

| Note | \($WHATAP\_HOME/plugin/ActionScript.x 에 작성한 Java 코드\)에 전달할 ID \($id 로 전달됨\) |
| :--- | :--- |


* Default : \[**Null**\]
* Type : String
