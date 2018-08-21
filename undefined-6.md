# 사용자 가이드

### 애플리케이션 모니터링 {#user-content-애플리케이션-모니터링}

와탭 APM 모니터링 서비스는 SaaS\(Software as a Service\) 방식의 웹 애플리케이션 서버\(WAS, Web Application Server\) 모니터링 서비스 입니다. 사용자는 아래와 같은 서비스를 받을 수 있습니다.

* 프로젝트 단위로 서버를 그룹핑하여 서버를 관리할 수 있고, 그룹화된 WAS들의 성능 통계 정보를 관측할 수 있습니다.
* 서버의 성능을 튜닝할 수 있는 포인트를 찾을 수 있게 해주므로 장애로 이어질 수 있는 서버의 문제점을 조기에 해결할 수 있습니다. 장애로 이어질 수 있는 성능 지연이나 병목 현상이 있는 서버와 서버 내 트랜잭션을 파악할 수 있으며, 해당 트랜잭션의 프로파일링 정보를 통해 성능 개선 구간과 병목 원인을 파악하여 서버의 성능을 튜닝할 수 있습니다.
* 성능 전문가의 도움을 받을 수 있습니다. APM의 사용자 초대 기능을 활용하여 성능 전문가를 초대하여 성능 모니터링을 함께 할 수 있습니다. 와탭의 성능 전문가가 함께 성능을 모니터링하여 장애 및 성능 개선 포인트를 찾아 주기적으로 보내주는 리포트를 받아 보실 수 있습니다.
* 다양한 외부 서비스를 통해 실시간 성능 정보 알림을 받아 장애를 방지할 수 있습니다. 애플리케이션 서버의 상태에 따라 이벤트 알림을 받을 수 있는 알림 정책을 설정하여, 슬랙\(Slack\)과 같은 외부 서비스를 통해 성능 알림 정보를 받아볼 수 있습니다.

본 문서는 와탭의 웹 애플리케이션 성능 모니터링 서비스를 효과적으로 활용하기 위한 활용 가이드를 제공합니다.

* 설치와 시작 가이드를 통해 APM 실행 개요와 서비스 사용을 위해 필요한 빠른 환경 설정 방법을 가이드합니다.
* 프로젝트 관리 가이드를 통해 관리하는 서버들을 효율적으로 그룹화하고 그룹별 관리자를 할당하는 방법, 관리자 초대 방법과 서비스 사용량 확인 방법을 가이드 합니다.
* 서버의 성능 튜닝 포인트를 찾을 수 있도록 가이드 합니다.
  * 실시간 모니터링 가이드를 통해 최근 10분간 집계된 아래 성능 통계 정보를 활용하여 장애로 이어질 수 있는 서버 상태 원인을 파악할 수 있게 하며 이를 해결하여 장애를 예방할 수 있도록 가이드 합니다.
    * WAS 설치 및 가용 서버 수 현황
    * 총 방문자수, 요청 트랜잭션 수 대비 초당 종료된 트랜잭션 수, 응답시간
    * 초당 종료된 트랜잭션 수, 응답시간 대비 가용 CPU, Heap Memory 리소스양
    * 서버별 진행중인 트랜잭션 수와 트랜잭션의 진행시간으로 성능 지연 및 병목 현상 발생 여부 파악
    * 종료된 트랜잭션의 처리시간과 오류 발생 정보 맵을 통해 트랜잭션 분포 패턴에 따른 병목 원인 예측
  * Cube 분석 가이드를 통해 아래 데이터 기준으로 하루의 성능을 5분 단위로 상대적으로 비교한 결과를 한 화면에서 보며 성능 튜닝 포인트를 찾아갈 수 있는 방법을 가이드 합니다.
    * Active Transaction 개수
    * TPS
    * 총 방문자수
    * 응답시간
  * 성능 데이터 통계 정보 활용 가이드를 통해 아래 성능 데이터 기준으로 정해진 시간 단위로 성능 데이터 발생 정보를 확인하고 튜닝 포인트를 찾아갈 수 있도록 가이드 합니다.
    * Transaction
    * Error
    * Sql
    * RemoteHTTPCall
    * 클라이언트 IP
    * 클라이언트 브라우저
    * HITMAP
    * DailyCounter
* 개별 인스턴스의 JVM 환경 활용 가이드를 통해 아래와 같은 JVM 환경 정보를 확인하고, 동적으로 에이전트나 JVM의 환경값을 변경하고 그 결과를 확인할 수 있도록 가이드 합니다.

| 이름 | 설명 |
| :--- | :--- |
| Boot Environment | 애플리케이션이 실행될때 설정되는 환경변수 목록 확인 |
| Enviroment | 현재 실행되고 있는 애플리케이션이 환경변수 목록 확인 |
| Componets | 애플리케이션이 참조하는 외부 라이브러리 목록 확인 |
| Thread List | 현재 애플리케이션에서 실행되는 Thread 목록과 상태 확인 |
| Heap Histogram | 애플리케이션이 사용한 Heap Memory의 상세 내역 확인 |
| Loaded Classes | 애플리케이션에 Loded 된 Class 목록 확인 |
| Open Socket | 애플리케이션이 사용한 Network Socket 확인 |
| Config | 와탭 에이전트 의 설정을 변경 |
| System GC | 애플리케이션의 Garbage Collection 실행 |

* 보고서 활용 가이드를 통해 프로젝트 단위로 정해진 날짜와 시간의 성능 데이터를 출력해 보고서로 활용할 수 있도록 가이드 합니다.

#### 관리 {#user-content-관리}

와탭 APM 모니터링 서비스는 다수의 애플리케이션 서버를 프로젝트로 그룹화하여 관리합니다.[![650](https://github.com/jinronara/deleteme_2/raw/master/images/650.png)](https://github.com/jinronara/deleteme_2/blob/master/images/650.png)

**라이선스 확인/발급 및 에이전트 다운로드**

와탭 APM 모니터링 서비스를 이용하기 위해서는 프로젝트 단위의 라이선스를 발급받은 후 에이전트를 다운로드 받아 모니터링 대상 애플리케이션 서버에 설치해야 합니다.

와탭 APM 모니터링 설치 절차에 따라 프로젝트 생성 후, Management &gt; 에이전트 설치 메뉴를 통해 기 발급된 라이선스를 확인하거나 에이전트를 다운로드 받을 수 있습니다.

**에이전트 업데이트**

와탭 APM 모니터링 서비스를 이용하면서 에이전트 버전이 업데이트 되었을 경우 새로운 버전을 다운로드 받을 수 있습니다.

* 해당 기능은 whatap.agent.tracer-0.4.5 이상의 버전에서만 제공됩니다.

[![660](https://github.com/jinronara/deleteme_2/raw/master/images/660.png)](https://github.com/jinronara/deleteme_2/blob/master/images/660.png)Figure 1. 관리 &gt; 에이전트 업데이트 메뉴를 통해 에이전트 업데이트를 진행할 수 있습니다.[![670](https://github.com/jinronara/deleteme_2/raw/master/images/670.png)](https://github.com/jinronara/deleteme_2/blob/master/images/670.png)

**프로젝트 관리**

**사용자 관리**

와탭 APM 모니터링 서비스의 사용자 권한 그룹은 Super Admin / Admin / User로 구분되며 각 그룹별 사용자 및 고유 역할은 다음과 같으며, 공통으로 모니터링 수행 권한을 가집니다. Management &gt; Project 관리 메뉴를 통해 사용자 관리 메뉴에 접근 할 수 있습니다.

| 권한그룹 | 프로젝트 당 계정 수 | 모니터링 | 사용자 초대 | 사용자 권한 변경 | 사용자 삭제 | 프로젝트 삭제 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Super Admin | 1 | ✓ | ✓ | ✓ | ✓ | ✓ |
| Admin | 제한 없음 | ✓ | ✓ | ✓ | ✓ | ✗ |
| User | 제한 없음 | ✓ | ✗ | ✗ | ✗ | ✗ |

Super Admin

프로젝트 당 1개 계정, 사용자 초대, 사용자 권한 변경, 사용자 삭제, 프로젝트 삭제

* 와탭에 가입 후 프로젝트를 생성한 계정에 부여되는 권한으로 프로젝트 삭제를 포함하여 프로젝트에 대한 모든 권한을 가지게 됩니다. 사용자 초대를 통해 프로젝트에 계정을 추가하거나 변경/삭제 버튼을 통한 계정의 권한 변경/삭제가 가능합니다.
  * 사용자 초대 시에는 Admin 또는 User 그룹으로 초대 할 수 있습니다.
  * 권한 변경 시 Super Admin 권한으로의 변경은 제한되어 있습니다.
  * 사용자 삭제 시에는 로그인 계정 외의 계정만 삭제 할 수 있습니다.

admin

계정 수 제한 없음, 사용자 초대 권한

* 사용자 초대를 통해 프로젝트에 계정을 추가하거나 변경/삭제 버튼을 통한 계정의 권한 변경/삭제가 가능합니다.
  * 사용자 초대 시에는 Admin 또는 User 그룹으로 초대 할 수 있습니다.
  * 권한 변경 시 Super Admin 권한으로의 변경은 제한되어 있습니다.
  * 사용자 삭제 시에는 Super Admin 계정 및 로그인 계정을 제외한 계정만 삭제 할 수 있습니다.

user

계정 수 제한 없음

* 모니터링 전용의 계정으로, 프로젝트 관리 및 사용자 관리 권한이 부여 되지 않습니다.

**Open API**

수집중인 모니터링 정보를 별도로 활용하거나, 서버의 Scale Up/Out의 자동화를 위해 적용하고자 하는 경우 Open API를 통해 해당 정보를 추출할 수 있는 기능을 제공합니다. 관리 &gt; 프로젝트 관리에서 프로젝트 정보 영역의 API Token 값을 Open API 호출 시 HTTP Header 정보로 전송하여 수집된 정보를 획득할 수 있습니다.

**Open API 확인**

[![680](https://github.com/jinronara/deleteme_2/raw/master/images/680.png)](https://github.com/jinronara/deleteme_2/blob/master/images/680.png)

API Token 변경이 필요한 경우 “재발급” 버튼을 통하여 신규 발급 Token으로 갱신할 수 있습니다.

**Open API 호출**

Open API 호출 시에는 Header 정보로 API Token 값과 Project Code를 전송합니다.

```text
curl -w "\n" -H "x-whatap-token: J************************A" -H "x-whatap-pcode: 1**1" "https://apm.whatap.io/open/api/cpu"
```

**Open API Spec**

| 구분 | key | value | 비고 |
| :--- | :--- | :--- | :--- |
| 헤더 | x-whatap-token | 프로젝트 단위의 API Token | 관리 &gt; 프로젝트 관리 |
| 헤더 | x-whatap-pcode | 프로젝트 코드 | 모니터링 수행 시의 URL에서 확인 가능[https://apm.whatap.io/project/apm/{프로젝트](https://apm.whatap.io/project/apm/%7B%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8) 코드}/dashboard[https://apm.whatap.io/v2/project/apm/{프로젝트](https://apm.whatap.io/v2/project/apm/%7B%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8) 코드}/dashboard |
| URL | [https://apm.whatap.io/open/api/act\_agent](https://apm.whatap.io/open/api/act_agent) | 활성화 상태인 에이전트 수 |  |
| URL | [https://apm.whatap.io/open/api/inact\_agent](https://apm.whatap.io/open/api/inact_agent) | 비활성화 상태인 에이전트 수 |  |
| URL | [https://apm.whatap.io/open/api/host](https://apm.whatap.io/open/api/host) | 물리 호스트 수 |  |
| URL | [https://apm.whatap.io/open/api/cpucore](https://apm.whatap.io/open/api/cpucore) | 물리 호스트의 CPU 코어 합 |  |
| URL | [https://apm.whatap.io/open/api/txcount](https://apm.whatap.io/open/api/txcount) | 트랜잭션 수 |  |
| URL | [https://apm.whatap.io/open/api/tps](https://apm.whatap.io/open/api/tps) | 초당 트랜잭션 수 |  |
| URL | [https://apm.whatap.io/open/api/user](https://apm.whatap.io/open/api/user) | 5분간 집계된 고유 사용자 수 |  |
| URL | [https://apm.whatap.io/open/api/actx](https://apm.whatap.io/open/api/actx) | 액티브 트랜잭션 수 |  |
| URL | [https://apm.whatap.io/open/api/rtime](https://apm.whatap.io/open/api/rtime) | 평균 응답 시간 |  |
| URL | [https://apm.whatap.io/open/api/cpu](https://apm.whatap.io/open/api/cpu) | CPU 사용률 |  |

**이벤트 설정**

애플리케이션 서버의 모니터링 정보에 임계치를 지정하여 실시간 모니터링 정보 기반의 Push 알림 기능을 제공합니다. 이벤트 알림은 에이전트의 모니터링 데이터 송신 주기\(5초\)에 전송된 데이터를 기반으로 서버에서 통지 여부를 판정하여 사용자에 통지하는 방식으로 이루어집니다.

이벤트 알림을 위한 설정은 관리 &gt; 이벤트 설정 메뉴를 통해 설정합니다.

**옵션 설명**

[![690](https://github.com/jinronara/deleteme_2/raw/master/images/690.png)](https://github.com/jinronara/deleteme_2/blob/master/images/690.png)

이벤트 알림 수단으로 이메일, Telegram, Slack을 활용 할 수 있으며, 애플리케이션 서버와 모니터링 수집 서버 사이의 네트워크 단절 등으로 인한 모니터링 정보 수집 불가시 애플리케이션의 다운 알림 수신 여부를 선택 할 수 있습니다.



* 모니터링 정보가 전송되지 않을 경우 애플리케이션의 다운 알림을 수신하고자 하는 경우, 애플리케이션 비활성 경고 &gt; 이후 드롭다운 목록을 선택하여 몇 초간 모니터링 정보가 수집되지 않았을 때 알림을 수신 할 지 선택하고, Enable 체크박스를 체크합니다.

이벤트 알림 설정을 위해 활용 가능한 모니터링 항목과 설정 가능 값은 다음과 같습니다.

| 이름 | 설명 |
| :--- | :--- |
| CPU | 애플리케이션 서버의 CPU 점유율의 warning 임계치\(%\), fatal 임계치\(%\) 및 지속 시간\(초\) |
| Disk | 디스크 사용률의 warning 임계치\(%\), fatal 임계치\(%\) 및 지속 시간\(초\) |
| Memory | 메모리 사용률의 warning 임계치\(%\), fatal 임계치\(%\) 및 지속 시간\(초\) |
| 히트맵 | 히트맵상의 같은 시간에 2.초 이상의 수직라인 발생시 전체시간 대비 차지하는 warning 비율\(%\), fatal 비율\(%\) 및 지속 시간\(초\) |
| Active Transaction | 실시간 트랜잭션 수의 상한 또는 하한\(부등식으로 지정\)과 지속 시간\(초\) |
| 에러 | 실시간 에러 트랜잭션 수의 상한 또는 하한\(부등식으로 지정\)과 지속 시간\(초\) |
| 반복 | 해당 이벤트 가 몇 초간 반복적으로 일어날 때 알림을 발생시켜야 하는지 시간\(초\)을 지정합니다. |
| 무음 | 이벤트 알림 후 다음 이벤트 알림까지의 최소 대기 시간\(초\)를 지정합니다. |

* 예를 들어 CPU 70%가 30초 동안 유지될 경우 알림을 받고 싶은 경우 Repeat을 30sec로 설정합니다. 해당 설정 값이 단 한번이라도 발생시 알림을 받고 싶은 경우 Repeat을 데이터 수집주기인 5sec로 설정합니다.
* 지나치게 빈번한 이벤트 알림을 방지하고 사용자가 이벤트의 심각성을 간과하게 될 가능성을 줄이기 위해서 적절한 대기 시간\[Silent\]을 설정해야 합니다.

**메일 설정**

이메일 알림을 활성화 하고자 하는 경우, User Email 에서 메일을 발행하고자 하는 이메일 주소의 좌측 체크박스를 체크합니다.[![700](https://github.com/jinronara/deleteme_2/raw/master/images/700.png)](https://github.com/jinronara/deleteme_2/blob/master/images/700.png)

**SNS 설정**

**Telegram 설정**

Telegram을 통하여 알림을 받고자 하는 경우 먼저 관리 &gt; 이벤트 설정에서 채널 탭의 Telegram의 체크박스를 체크한 후 저장을 합니다.

이후 Telegram에 @WhaTapApmNotiBot 을 검색합니다.[![710](https://github.com/jinronara/deleteme_2/raw/master/images/710.png)](https://github.com/jinronara/deleteme_2/blob/master/images/710.png)

검색 후 나오는 Bot을 선택한 뒤 시작 버튼을 누릅니다.[![720](https://github.com/jinronara/deleteme_2/raw/master/images/720.png)](https://github.com/jinronara/deleteme_2/blob/master/images/720.png)

이후 채팅창에 알림을 받을 프로젝트의 라이선스 키를 입력합니다.[![730](https://github.com/jinronara/deleteme_2/raw/master/images/730.png)](https://github.com/jinronara/deleteme_2/blob/master/images/730.png)

* 해당 프로젝트의 라이선스는 관리 &gt; 프로젝트 관리에서 다시 확인 가능합니다.
* 사용 가능한 명령어 목록
  * /help : 명령어 목록 보기
  * /license : 알림 받을 프로젝트의 라이선스 넣기
  * /remove : 알림을 받지 않을 프로젝트 코드 넣기
  * /list : 현재 알림을 받고 있는 프로젝트 코드들 보기

**Slack 설정**

* Slack을 활용하여 이벤트 알림을 수신하고자 하는 경우, Channels 목록에서 Slack 체크박스를 체크합니다.
* 다음으로 Add to Slack 버튼을 클릭하여 Slack의 팀 및 채널에 WhaTapNotiBot이 통지를 전파 할 수 있도록 권한을 부여합니다.

[![740](https://github.com/jinronara/deleteme_2/raw/master/images/740.png)](https://github.com/jinronara/deleteme_2/blob/master/images/740.png)

**미터링 확인**

와탭 APM 모니터링 서비스는 CPU 코어 단위의 과금 체계를 적용합니다. 모니터링 정보의 수집 대상인 애플리케이션 서버가 탑재된 물리 서버의 CPU 코어 정보를 탐지하여 월간 추이를 수집하여 차트로 나타내고 상세 정보를 제공합니다.Metering Information

일간 최대 CPU 코어 수를 기준으로 월간 CPU 코어 추이를 차트로 표시합니다.[![750](https://github.com/jinronara/deleteme_2/raw/master/images/750.png)](https://github.com/jinronara/deleteme_2/blob/master/images/750.png)Monthly Table

일간 최대 CPU 코어 수를 기준으로 월간 CPU 코어 테이블을 표시합니다.

| 일자\(UTC 기준\) | 년월일 |
| :--- | :--- |
| CPU 코어 수 | 전체 코어 수 |
| 에이전트 수 | 전체 에이전트 수 |
| 호스트 수 | 전체 호스트 수 |

[![760](https://github.com/jinronara/deleteme_2/raw/master/images/760.png)](https://github.com/jinronara/deleteme_2/blob/master/images/760.png)Daily Table

월간 추이 차트의 일 정보 클릭 시, 하단에 시간당 최대 CPU 코어 수를 기준으로 일간 CPU 코어 테이블이 표시됩니다.

| 일자\(UTC 기준\) | 년월일시 정보 |
| :--- | :--- |
| CPU 코어 수 | 시간대별 최대 코어 수 |
| 에이전트 수 | 시간대별 최대 에이전트 수 |
| 호스트 수 | 시간대별 최대 호스트 수 |

[![770](https://github.com/jinronara/deleteme_2/raw/master/images/770.png)](https://github.com/jinronara/deleteme_2/blob/master/images/770.png)

#### 실시간 모니터링 {#user-content-실시간-모니터링}

모니터링 대상 서버로부터 실시간으로 수집되고 있는 정보를 통해 프로젝트의 성능 현황을 전체적으로 확인하기 위한 정보를 제공합니다. 즉각적인 대응이 가능하며 잠재적으로 증가 하고 있는 문제를 파악할 수 있습니다.

**대시보드를 통한 시스템 전체 현황 파악**

모니터링 대상 서버로부터 실시간으로 수집되고 있는 정보의 현황을 대시보드를 통해 확인할 수 있습니다. CPU, Memory를 제외한 일반적인 차트는 안정적인 데이터는 파란색으로 표현하며 그 외에 문제라 예측할 만한 색은 붉은 계열로 표시되어 사용자가 쉽게 파악할 수 있습니다.[![780](https://github.com/jinronara/deleteme_2/raw/master/images/780.png)](https://github.com/jinronara/deleteme_2/blob/master/images/780.png)

대시보드를 통해 제공하는 정보는 아래와 같습니다.

* 수집대상 서버 및 비활성 서버 수
* 수집대상 서버의 전체 Core 수
* 수집대상 서버의 호스트 수
  * 시각화 정보를 출력할 대상 서버를 설정을 통해 필터링 하기 위한 기능을 제공합니다.
* 액티브 트랜잭션 수 - 수집 대상 서버 단위로 실행 중 트랜젝션을 시각화하여 원형 Chart로 제공합니다.
* 실행 상태의 트랜잭션 수 및 URL 리스트를 확인하기 위한 링크를 제공합니다.
* 히트맵 - 시간대 별 트랜잭션 수행 시간 분포를 XY-Chart 형태로 제공합니다. 추가로 트랜잭션 수행 시간 범위를 확장/축소 가능합니다.
  * User - 실시간으로 접속 중이 유저 추이를 시간 흐름에 따른 Chart 및 접속 지역 Chart를 제공합니다. 서버 인스턴스 단위 상세 페이지에의 링크를 제공합니다.
  * Transaction - 초당 트랜잭션 추이 및 응답 속도 Chart를 제공합니다. 서버 인스턴스 단위 상세 페이지에의 링크를 제공합니다.
  * Resource - 호스트 단위의 CPU 사용률 및 Heap 메모리 사용량의 추이를 Chart로 제공합니다. 서버 인스턴스 단위 상세 페이지에의 링크를 제공합니다.

**진행 중 트랜잭션**

현재 진행중인 트랜잭션을 면밀히 관찰하기 위해서 다음의 두 가지 차트를 제공하고 있습니다. 액티브 트랜잭션은 TPS의 정보를 표현하며 히트맵은 요청을 처리한 시간을 표현합니다.[![790](https://github.com/jinronara/deleteme_2/raw/master/images/790.png)](https://github.com/jinronara/deleteme_2/blob/master/images/790.png)

* Arc Equalizer 차트
* 히트맵 차트

**액티브 트랜잭션**

액티브 트랜잭션은Arc Equalizer차트를 사용 중이며, 기본적으로 현재 진행중인 요청의 수를 확인할 수 있습니다. 5초마다 현재 서버에서 처리 중인 요청의 수를 표현해서 해당 요청이 각각 어느 정도의 시간동안 처리 중인지 알 수 있습니다. 5초 간격의 시간에 감지된 요청들은 위험 여부도 파악할 수 있도록 다음과 같이 색으로 분류됩니다.

* 0초 ~ 3초: 파란색
* 3초 ~ 8초: 군청색
* 8초 이상: 빨간색

파란색이 많이 표현되는 것은 크게 문제가 되지 않지만 이는 아직 진행중이므로 이중에 일부가 보라색이나 빨간색으로 바뀌어 표현될 가능성이 있으므로 추이를 지켜봐야 합니다.[![800](https://github.com/jinronara/deleteme_2/raw/master/images/800.png)](https://github.com/jinronara/deleteme_2/blob/master/images/800.png)

또한 5초 간격으로 감지를 하기 때문에 서버가 정상적인 처리를 하고 있음에도 응답시간이 낮아서 액티브 트랜잭션에는 표시가 안될 수가 있습니다. 이를 방지하기 위해서 액티브 트랜잭션 둘레에는 5초 동안 정상적인 처리를 하고 있음을 표현하기 위해 두 개의 바가 회전을 하고 있습니다. 5초 사이의 사용량에 따라서 느림, 중간, 빠름의 속도로 차트 주변을 회전하게 됩니다. 회전 속도는 발생되는 문제점을 표현하는게 아니라 사용량이 많아진다는 것을 표현합니다.

액티브 트랜잭션의 옆에 화살표를 클릭하면 현재 진행중인 실시간 트랜잭션을 세부적으로 파악 할 수 있습니다.[![810](https://github.com/jinronara/deleteme_2/raw/master/images/810.png)](https://github.com/jinronara/deleteme_2/blob/master/images/810.png)

좌측에는 애플리케이션 서버의 리스트와 진행중인 트랜잭션을 정상, 느림, 매우 느림의 개수로 표현하며 해당 서버를 선택하게 되면 우측에 세부정보가 표현됩니다.

화면에 표시되는 요약 정보의 표시 항목은 다음과 같습니다.

| 시작 시간 | 트랜잭션의 시작 시간 |
| :--- | :--- |
| 경과 시간 | 요청을 처리하는데 걸린 시간 |
| URL | 호출 URL |

우측의 액티브 트랜잭션 리스트에서 조금 더 자세한 정보를 원한다면 해당 트랜잭션을 클릭하면 세부사항이 표시됩니다.[![820](https://github.com/jinronara/deleteme_2/raw/master/images/820.png)](https://github.com/jinronara/deleteme_2/blob/master/images/820.png)

| 이름 | 설명 |
| :--- | :--- |
| 애플리케이션 | 애플리케이션 서버 명\(에이전트 단위의 식별자\) |
| 시작 시간 | 액티브 스택 취득 시간 |
| 경과 시간 |  |
| 메모리 할당 |  |
| CPU 시간 | CPU 사용 시간 |
| SQL 개수 | SQL 발행 횟수 |
| SQL 시간 | SQL 수행 시간 |
| HTTP 요청개수 | 아웃바운드 Http Call 수 |
| HTTP 요청시간 | 아웃바운드 Http Call 시간 |
| 클라이언트 IP |  |
| 데이터베이스 커넥션 | DB 접속 URL |

**응답 시간 분포도 \(히트맵\)**

히트맵 차트는 현재 처리 되고 있는 요청이 완료되면 점으로 표현합니다. 가로축은 시간을 나타내며 세로축은 요청을 처리한 시간을 표현함으로 급격하게 느려진 트랜잭션이 존재한다면 상위에 노출 될 것입니다. 차트는 상하로 최소 5초 최대는 80초까지 표시됩니다. 또한 에러가 발생하는 경우에는 점을 빨간색으로 표시하여 조금 더 명확하게 인지할 수 있습니다. 모든 서버의 트랜잭션이 수집되며 정상범위 중에 일정시간 이하의 트랜잭션은 무시됩니다. 일정시간 이하의 정보 또한 수집하고 싶다면 JVMP &gt; Server \(More버튼\) Config 설정에서 수치를 낮춰주면 수집이 가능합니다.[![830](https://github.com/jinronara/deleteme_2/raw/master/images/830.png)](https://github.com/jinronara/deleteme_2/blob/master/images/830.png)

히트맵 차트에서는 우측 상단에 애플리케이션 서버를 필터링 할 수 있는 버튼이 있습니다. 기본적으로는 모든 서버의 트랜잭션을 보여주지만 서버가 많아질 경우 원하는 서버만을 체크해서 볼 수 있습니다.

차트에서는 자세히 보기 기능을 제공합니다. 마우스를 드래그 하여 자세히 봐야할 점들을 포함하여 드래그를 하게 되면 점들이 표시하는 트랜잭션 정보들을 조금 더 자세히 볼 수 있는 화면으로 넘어가게 됩니다.[![840](https://github.com/jinronara/deleteme_2/raw/master/images/840.png)](https://github.com/jinronara/deleteme_2/blob/master/images/840.png)

히트맵 Transaction Summary 화면은 사실상 메뉴의 Cube 활용 / 분석 &gt; 히트맵 메뉴와 동일한 기능을 합니다. 단지 사용자가 선택해서 들어온 부분에 대한 집중을 하기 위해서 선택된 시간을 위주로 표현합니다. 이렇게 사각형으로 각 서버의 처리량을 표현하면서 일차적으로는 동일 기능을 한다면 적절하게 분배가 되고 있는지도 확인이 가능합니다. 선택된 점들을 중심으로 하단에는 각 서버당 Transaction의 숫자를 표현하며 에러가 존재한다면 빨간색으로 표현합니다. 하단의 사각형으로 표시된 서버를 선택하게 되면 가장 오래된 시간을 기준으로 각각의 Transaction 세부 사항들을 우측에 리스트로 나타납니다.

Transaction List는 세부적인 정보를 가지고 있습니다. List 에서 원하는 Transaction을 선택하게 되면 해당 Transaction의 세부적인 정보와 처리 순서를 보여주게 되는데 이는 Cube 활용, 분석 &gt; 히트맵과 통계 &gt; Transaction 에서 자세히 설명하겠습니다.

**트랜잭션 분포**

**프로파일 분석**

**트랜잭션 연계 추적**

* 멀티서버 트랜잭션

서비스\(업무\) 별로 분리 되어 있는 애플리케이션 서비스들간의 호출을 추적할 수 있습니다. 와탭에 등록되어 있는 프로젝트라면 프로젝트에 등록된 애플리케이션 서비스들간의 호출에 대한 추적을 말합니다

멀티서버 트랜잭션 추적 옵션을 설정한 경우에 한하여 트랜잭션 연계 추적이 가능합니다. \(옵션명 mtrace\_rate\)[![850](https://github.com/jinronara/deleteme_2/raw/master/images/850.png)](https://github.com/jinronara/deleteme_2/blob/master/images/850.png)

* 트랜잭션에서 외부 호출을 하는 경우에도 동일한 MTID가 생성됩니다.
* 업무별로 프로젝트가 분리 되어 있더라도 처음 발급한 MTID를 통해 애플리케이션간의 모든 트랜잭션을 확인 할 수 있습니다.

[![860](https://github.com/jinronara/deleteme_2/raw/master/images/860.png)](https://github.com/jinronara/deleteme_2/blob/master/images/860.png)

동일한 MTID를 갖는 트랜잭션 서비스들 목록과, 특정 트랜잭션의 프로파일 정보를 확인 할 수 있습니다.콜러와 콜리

같은 프로젝트에 속한 애플리케이션 서비스들간의 호출관계는 콜러와 콜리기능을 통하여 프로파일 데이터를 바로 확인 할 수 있습니다.

* 콜리: 서비스를 호출한 트랜잭션
* 콜러: 서비스를 호출 당한 트랜잭션

[![870](https://github.com/jinronara/deleteme_2/raw/master/images/870.png)](https://github.com/jinronara/deleteme_2/blob/master/images/870.png)[![880](https://github.com/jinronara/deleteme_2/raw/master/images/880.png)](https://github.com/jinronara/deleteme_2/blob/master/images/880.png)[![890](https://github.com/jinronara/deleteme_2/raw/master/images/890.png)](https://github.com/jinronara/deleteme_2/blob/master/images/890.png)

**처리량 및 응답시간**

모니터링 대상 서버가 초당 어느 정도의 처리를 하고 있는 지에 대한 정보 현황을 그래프로 확인 할 수 있습니다. 해당 그래프는 모니터링 하고 있는 모든 서버의 합을 표시해주며 그래프의 높낮이를 통해 급격한 증가 및 감소를 확인 할 수 있습니다. 서버가 처리하는 단순한 양은 성능에 대한 절대적인 수치를 확인할 수 없으므로 응답시간과 함께 확인해야 합니다. 응답시간은 서버가 요청을 받아서 응답을 줄 때까지의 시간을 나타냅니다. 모든 서버들의 응답시간을 평균을 나타내기 때문에 서버의 전체적인 성능 저하가 발생 했을 때 손쉽게 확인이 가능합니다. 전체적인 정보와 달리 적은 숫자의 긴 응답시간은 히트맵에 표시 되기 때문에 히트맵 의 세부사항에서 확인해야 합니다.[![900](https://github.com/jinronara/deleteme_2/raw/master/images/900.png)](https://github.com/jinronara/deleteme_2/blob/master/images/900.png)

각 헤더를 클릭하면 서버당 데이터를 보여주는 차트를 확인할 수 있습니다. 우측에 애플리케이션 서버를 리스트로 표현하며 원하는 특정 서버를 확인하고 싶다면 체크를 통해 확인을 할 수 있습니다. 애플리케이션 서버 중 일부 서버가 CPU 집중적인 작업을 수행할 경우 실시간으로 이를 파악 할 수 있습니다.[![910](https://github.com/jinronara/deleteme_2/raw/master/images/910.png)](https://github.com/jinronara/deleteme_2/blob/master/images/910.png)[![920](https://github.com/jinronara/deleteme_2/raw/master/images/920.png)](https://github.com/jinronara/deleteme_2/blob/master/images/920.png)

우측에 애플리케이션 서버를 리스트로 표현하며 원하는 특정 서버를 확인하고 싶다면 체크를 통해 확인을 할 수 있습니다. 애플리케이션 서버 단위의 Heap 메모리 사용과 GC 발생 추이, 메모리 leak 감지 등을 실시간으로 파악하는데 활용 가능하겠습니다.

**사용자 접속 추이**

**수집 기준**

**자원 사용 추이**

애플리케이션이 실행되고 있는 하드웨어의 CPU 사용률과 메모리 사용량을 모니터링 할 수 있습니다. 5초 간격으로 수집을 하며 최근 10분간의 데이터만을 차트로 시각화 합니다. 라인차트로 표현되기 때문에 많은 양의 서버가 표현된다고 해도 문제가 있는 서버 만을 파악할 수 있습니다. 자원 사용량은 CPU와 Memory 정보로 나눠 표현됩니다.

**CPU 사용률 추이**

CPU 정보는 100% 를 기준으로 모든 서버가 표현됩니다. 서버가 많아지더라도 위험수치에 다다른 서버들이 있다면 상위로 표시 되기 때문에 문제가 생기는 서버만을 손쉽게 알 수 있습니다. 실시간 정보이기에 CPU 가 점점 올라가는 상황을 파악할 수 있으며 즉각적으로 문제점을 찾을 수 있습니다.[![930](https://github.com/jinronara/deleteme_2/raw/master/images/930.png)](https://github.com/jinronara/deleteme_2/blob/master/images/930.png)

**힙 메모리 사용률 추이**

메모리는 각 서버당 사용가능한 최대 메모리 와 현재 사용중인 메모리를 보여줌으로써 위험수치에 있는 서버를 알 수 있으며 시간에 따른 메모리 사용량을 실시간으로 볼 수 있습니다.

* 메모리 라인 차트는 보통 계속해서 물결 치며 이는 애플리케이션 서버가 요청을 처리 하기 위해 메모리를 사용할 때 증가하며 GC를 통해서 메모리를 정리할 경우에 감소합니다.

[![940](https://github.com/jinronara/deleteme_2/raw/master/images/940.png)](https://github.com/jinronara/deleteme_2/blob/master/images/940.png)

#### 스택 분석 {#user-content-스택-분석}

10초 간격으로 수집된 Java Thread Dump를 분석하여 Cube 구간에 장시간 정체되어 있던 Stack 상의 Step\* 정보를 제공하는 것을 목적으로 Stack 전체 기준의 통계\(Unique Stack\)와 최상위 Step 기준의 통계\(Top Stack\) 제공합니다.Step

Thread Dump의 단위 Stack Trace 상의 클래스 호출 단위

또한 각 트랙잭션별로 Active Stack 정보를 알 수 있습니다. 트랜잭션에서 실행하고 있던 Stack 정보를 수집하고 분석하여 이슈를 찾는 데 도움을 얻을 수 있습니다. Top Stack과 Unique Stack은 각각의 수집 기준이 상이하므로, 분석 정보간의 상호 연관성을 검토하여 성능 정보에 대한 분석 결과로 활용할 필요성이 있습니다.탑 스택

최상위 Step의 적체 비율 및 Step 간의 호출 비율유니크 스택

전체 Step의 적체 비율

**액티브 스택**

ActiveStack 차트는 5분 간의 단위 통계 데이터를 Active Transaction의 수를 막대로, TPS를 꺾은선으로 표시합니다.[![950](https://github.com/jinronara/deleteme_2/raw/master/images/950.png)](https://github.com/jinronara/deleteme_2/blob/master/images/950.png)

막대를 클릭하면, 클릭한 시간대의 Active Transaction의 정보가 나오며, 그 정보를 클릭하면 해당 Transaction의 ActiveStack을 볼 수 있습니다.[![960](https://github.com/jinronara/deleteme_2/raw/master/images/960.png)](https://github.com/jinronara/deleteme_2/blob/master/images/960.png)

**탑 스택**

Stack Trace 상의 각 Step 기준으로, Step과 Step간의 호출 비율을 백분율로 분석한 정보를 제공합니다. 최상위 Step의 적체 빈도를 백분율로 산출하여 내림차순으로 정렬한 결과를 제시합니다. 각 Step을 클릭하면 해당 Step을 호출하는 상위 Step을 호출 빈도 기준 백분율로 산출하여 제시합니다.

Top 스택 통계는 충분히 많은 데이터를 가지고 판단하는 것이 좋습니다. 따라서 하루 단위의 스택을 조회하는 것을 추천하며, 스택의 개수가 1~2건일 시 통계적인 의미를 갖기에는 부족할 수 있습니다. Top 스택은 튜닝 시 인지 하기 힘들었던 부분의 튜닝 포인트를 찾아내는 것에 유용합니다. 가장 빈번하게 나타난 스택은 현재 애플리케이션 서버에서 가장 많은 부하를 발생하는 것이라고 판단 할 수 있습니다. 가장 왼쪽의 나타나는 비율은 애플리케이션 서버 성능에 영향을 미치는 정도라고 할 수 있습니다. 안정적인 애플리케이션 서버일지라도 빈번하게 나타난 스택은 성능 저하를 일으킬 수 있는 가능성이 있으므로 해당 클래스는 유심히 보는 것이 좋습니다. Top 스택 클릭 시 해당 최상위 스택에 대한 호출 빈도를 확인할 수 있습니다. Top 스택의 호출관계는 1대1 관계이므로 depthTop 스택은 가 밑으로 내려갈수록 정보의 정확성이 떨어질 수 있습니다. 하위 depth에 대한 정보는 참고 용도로 사용하며 튜닝을 진행하시기 바랍니다. 애플리케이션 성능 개선을 위해 최상위 Step의 적체 비율이 높은 모듈의 병목 가능성 검토 할 필요가 있습니다. 적체 비율이 높은 모듈의 경우 작은 성능 개선도 애플리케이션 전체에 상당한 개선 효과를 가져올 수 있습니다.[![970](https://github.com/jinronara/deleteme_2/raw/master/images/970.png)](https://github.com/jinronara/deleteme_2/blob/master/images/970.png)

* \(주의\) Top Stack을 통해 호출 비율을 판단 할 경우, Step간 호출 비율을 곱하여 전체 호출 관계 비율을 산출해서는 안됩니다. Top Stack의 호출 비율은 Stack Trace 상에 노출된 정보의 Step간 호출 비율의 산출 결과이기 때문에, Step간 호출 비율로 전체 호출 비율을 도출할 경우 왜곡된 결과를 도출하게 됩니다.
* Ex\) whatap.util.ThreadUtil.sleep ← jdbc.Control.exec 의 호출 비율은 87.10% jdbc.Control.exec ← jdbc.FakePreparedStatement.executeQuery 의 호출 비율은 61.18%
* 단, whatap.util.ThreadUtil.sleep ← jdbc.Control.exec ← jdbc.FakePreparedStatement.executeQuery 의 호출 비율이 87.10% \* 61.18% 를 의미하지는 않음. \(jdbc.Control.exec에서 타 모듈의 호출 가능성이 존재하기 때문임\)

**유니크 스택**

Stack Trace 전체의 Hash 값 기준의 산출 결과로 전체 Step이 동일한 호출 비율을 백분율로 분석한 정보를 제공합니다. Top Stack이 Step 간의 호출 비율에 대한 정보를 제공하는 것과 달리, Unique Stack은 Stack Trace 전체의 정확한 호출 정보를 기반으로 한 데이터를 제공하므로, 상세 호출 관계를 파악하는 데 유용한 정보를 제공합니다.

* 적체 비율이 높은 Stack Trace 식별 할 수 있습니다.

상세 호출 Step 검토를 통한 호출 경로 상에 이상 모듈의 존재 여부를 파악 할 수 있습니다.[![980](https://github.com/jinronara/deleteme_2/raw/master/images/980.png)](https://github.com/jinronara/deleteme_2/blob/master/images/980.png)

**힙 스택**

{text 힙스택 관련 내용 필요}

#### 사후 분석 {#user-content-사후-분석}

**Cube**

Cube는 5분 간의 수집 정보 통계를 활용한 애플리케이션 상세 분석 정보를 제공합니다. Cube는 1일을 5분 구간으로 분할하여 288개의 Cube 단위 통계로 실시간 사용자, 국가별 접속, Hit Map 트랜잭션, TOP 트랜잭션, TPS, 응답 시간, 자원 사용 정보를 제공합니다.

**Cube 활용**

Cube는 서버에 전송된 데이터의 5분 단위 통계 데이터를 시각화하여 제공합니다. Cube 대시보드는 상단에 일시 선택 기능을 제공하여, 사용자는 이를 통해 5분 단위의 통계 구간을 지정하여 모니터링 정보를 확인 할 수 있습니다. 아울러 대시보드 좌측의 Cube 단위 밀도 차트의 Cube Cell을 선택하여 구간을 지정 할 수도 있습니다.[![990](https://github.com/jinronara/deleteme_2/raw/master/images/990.png)](https://github.com/jinronara/deleteme_2/blob/master/images/990.png)Cube 차트

Cube 차트의 Cell은 통계 정보의 밀도 또는 크기를 색상으로 시각화하여 표현합니다.[![1000](https://github.com/jinronara/deleteme_2/raw/master/images/1000.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1000.png)

Cube 차트의 밀도 표시 기준으로 다음 옵션을 선택 할 수 있습니다.

* 본 제품은 MaxMind사의 GeoLite2를 사용하고 있으며, 이에 따른 라이센스 정책을 준수하고 있습니다. GeoLite2는 [http://www.maxmind.com에서](http://www.maxmind.xn--com-k94n91q/) 확인할 수 있습니다. \(This product includes GeoLite2 data created by MaxMind, available from [http://www.maxmind.com](http://www.maxmind.com/)\)

| Active Tx 개수 | 실행 상태의 트랜잭션 수 중 최대값 |
| :--- | :--- |
| TPS | 5분간의 TPS |
| 실시간 사용자 | 실행 상태에 있던 트랜잭션과 연관된 사용자 수, 실제 애플리케이션을 사용중인 사용자 수로 식별 가능한 정보 |
| 응답시간 | 평균 응답 시간 |
| User | Cube Cell 구간의 최대 사용자 수와 접속 국가 수를 요약 정보로 제공하고, 실시간 사용자 수 추이와, 국가별 request 수를 표현합니다. |
| Transaction | Cube Cell 구간의 평균 TPS와 평균 응답속도를 요약 정보로 제공하고, 트랜잭션 추이와 평균 응답속도의 추이를 차트로 제공합니다. |
| Resource | Cube Cell 구간의 평균 CPU 사용률과 Max Core 수를 요약 정보로 제공하고, 호스트 단위 평균 CPU 사용률과 애플리케이션 단위 Heap 메모리 사용률을 차트로 상위 5개 항목에 대하여 제공합니다. |
| CPU\(TOP 5\) | 애플리케이션 단위 일간 5분간의 CPU 사용률 추이\(5초 정보 기준\) |
| Heap Memory\(TOP 5\) | 애플리케이션 서버 단위 5분간의 Heap 메모리 사용률 추이\(5초 정보 기준\) |

* Active Tx : 트랜잭션의 시작~종료 구간 중 일부가 수집 구간에 포함된 트랜잭션
* TPS : Transaction Per Seconds

| 일일 합계 | 프로젝트 단위 일간 트랜잭션 추이\(5분 정보 기준\) |
| :--- | :--- |
| 전체 큐브 | 애플리케이션 서버 단위 5분간 트랜잭션 추이\(5초 정보 기준\) |

**성능 추이 분석**

성능 추이에서는 지정한 시간에 해당하는 성능에 영향을 끼치는 정보들을 조회할 수 있습니다. 성능 추이에 조회할 수 있는 정보로는 실시간 사용자, 트랜잭션/초\(합계\), 응답시간, CPU, 힙 메모리 , 액티브 TX등의 정보와 많이 처리된 트랜잭션\#10, HTTP Call\#10, SQL\#10 등의 정보를 조회할 수 있습니다. 또한 전체, 개별 애플리케이션 서버 별로 그래프를 확인할 수 있어 성능에 많은 영향을 끼치는 애플리케이션 서버가 무엇인지도 쉽게 알 수 있습니다.[![1010](https://github.com/jinronara/deleteme_2/raw/master/images/1010.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1010.png)

화면에 표시되는 요약 정보의 표시 항목은 다음과 같습니다.

| 이름 | 설명 |
| :--- | :--- |
| 실시간 사용자 | 실시간으로 방문한 사용자 수 |
| 트랜잭션/초\(합계\) | 처리된 트랜잭션의 개수 합 |
| 응답시간 | 응답시간의 평균 |
| CPU | CPU 사용량의 평균\(%\) |
| 힙 메모리 | 힙 메모리의 사용량 |
| 액티브 TX | 실행 상태의 트랜잭션 수 |
| 트랜잭션 \#10 | 가장 많이 처리된 트랜잭션의 상위 10개 |
| HTTP Call \#10 | HTTP Call 상위 10개 |
| SQL \#10 | 가장 많이 호출된 SQL Query 상위 10개 |

**히트맵 분석**

[![1020](https://github.com/jinronara/deleteme_2/raw/master/images/1020.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1020.png)

히트맵은 특정 기간 동안의 응답 시간 분포를 한눈에 파악 할 수 있는 분포 그래프 입니다. 트랜잭션 발생 위치에 따라 느린 트랜잭션을 쉽게 찾아 낼 수 있으며, 색상을 통하여 에러 발생여부에 대해서 또한 빠르게 찾아 낼 수 있습니다. 분석에서 히트맵은 짧게는 10분 길게는 일일로 지정하여 응답 시간 분포에 대해 조회할 수 있으며, 어느 시점에서 응답시간이 느렸는지, 에러가 많이 발생했는지에 대해 파악할 수 있는 지표가 됩니다. 또한 히트맵이 그려진 모양을 통해 문제의 원인을 파악할 수 있습니다. 전체, 애플리케이션 서버 별 히트맵을 볼 수 있어 애플리케이션 별 개선에 사용할 수 있습니다.

10분, 30분, 시간 단위로 히트맵은 선택한 시작 시간으로부터 각 지정된 시간 단위 동안의 응답시간 분포를 파악 할 수 있습니다. 5초 단위의 히트맵으로, 드래그시 선택한 기간과 응답시간 내에 발생한 트랜잭션을 조회할 수 있습니다. 조회한 트랜잭션은 클릭 시 프로파일 정보를 조회 할 수 있으며 스텝 정보를 볼 수 있습니다. 시간대 별로 응답시간이 느린 트랜잭션이 무엇인지 판단하는 것이 중요하며, 특정 시간에만 발생하는 트랜잭션인지에 대한 여부 또한 확인해 보아야할 사항입니다. 에러가 발생했다면 에러의 대한 원인이 연쇄반응으로 인하여 발생한지에 대한 여부 또한 파악해야 합니다.

일일 단위의 히트맵은 선택한 날짜에 대한 응답시간 분포를 파악할 수 있습니다. 5분 단위의 히트맵으로, 시간 별 추이를 파악하는데 사용합니다. 특정 시간대에 발생한 문제를 찾아낼 수 있으며, 다른 날짜의 히트맵과의 비교를 통해, 주기적으로 발생하는 문제가 아닌지 확인할 필요가 있습니다.

* 조건부: 조회하고자 하는 날짜와, 시작시간을 선택하여 원하는 과거의 히트맵 데이터를 조회할 수 있습니다. 애플리케이션 전체 및 개별 통계를 선택적으로 조회할 수 있습니다. 정렬 기준을 선택하여 데이터를 조회할 수 있으며, 필터 기능으로 원하는 데이터를 조회할 수 있습니다.
  * 카테고리 - 10분/30분/시간/일일 히트맵 선택
  * 날짜 - 히트맵 조회 시작 날짜 설정
  * 시간 - 히트맵 조회 시작 시각 설정
  * 분 - 히트맵 조회 시작 분 설정
  * 애플리케이션 - 전체, 개별 애플리케이션 서버 설정

**개별 지표 비교 분석**

**일일 카운터**

하루 동안 수집된 카운터 정보에 대한 그래프를 5분 단위로 조회할 수 있습니다. 카운터 정보는 트랜잭션, 사용자, 자원으로 구분하여 조회할 수 있습니다. Daily Counter 는 여러개의 그래프를 추가할 수 있어, 지표 별 비교가 가능하며, 일자별 비교 또한 가능합니다. 지표 별 비교는 성능 문제에 대한 원인을 통합적으로 분석할 수 있습니다. 예를 들어, TPS와 응답시간을 같이 보며 TPS에 따른 응답시간의 변화를 파악할 수 있으며, 자원에서 CPU의 변화와 GC Count, GC Time 등을 통해 CPU 사용에 대한 원인을 파악할 수 있습니다. 날짜별 비교에서는 평일, 휴일간의 비교, 프로모션 및 이벤트 기간의 비교 등 다양한 관점에서의 비교 분석이 가능 합니다. 또한 전체, 개별 애플리케이션 서버별로 그래프를 확인할 수 있어 애플리케이션 서버 별 비교 분석 또한 가능합니다. 자원사용량은 전체 분석 시 평균 처리로 인한여 데이터의 정확도가 떨어질 수 있으니 애플리케이션 서버별로 비교분석 하는 것이 좋습니다. Daily Counter 에서 조회할 수 있는 정보는 다음과 같습니다.Table 1. 트랜잭션

| 이름 | 설명 |
| :--- | :--- |
| TPS | 초당 트랜잭션 처리량 |
| 에러 개수 | 에러 발생 개수 합 |
| 응답 시간 | 평균 트랜잭션 응답 시간 |
| 액티브 트랜잭션 | 평균 진행 중 트랜잭션 개수 |
| Sql 개수 | SQL 실행 개수 합 |
| Sql 에러 | SQL 에러 개수 합 |
| Sql 시간 | SQL 수행 시간 합 |
| Sql 페치 | SQL Fetch 개수 합 |
| Sql 페치 시간 | SQL Fetch 시간 합 |
| HttpC 개수 | Http Call 개수 합 |
| HttpC 에러 | Http Call 발생 에러 개수 합 |
| HTTP 요청 시간 | 아웃바운드 Http Call 시간 |

Table 2. 사용자

| 이름 | 설명 |
| :--- | :--- |
| Realtime user | 실시간 방문 사용자 |

Table 3. 자원

| 이름 | 설명 |
| :--- | :--- |
| CPU | CPU 사용량 \(Machin CPU\) |
| CPU Max | CPU 사용량 최고치 |
| CPU sys | CPU System 사용량 \(%\) |
| CPU user | CPU User 사용량 \(%\) |
| CPU wait | CPU Wait 총 합 |
| Process CPU | Process의 CPU 사용량 총 합 |
| Heap total | Heap total 량 \(M\) |
| Heap used | Heap used 량 \(M\) |
| Heap perm | Heap perm 량 \(M\) |
| Heap pending finalization | Pending finalization 개수 |
| DB Connection Active | 활동중인 DB의 수 |
| DB Connection Idle | 활동하지 않고 접속중인 DB의 수 |
| DB Connection Total | 접속한 DB의 총 합 |
| GC count | GC Count 횟수 |
| GC time | GC 시간 총합 |
| GC time max | GC 시간 최고치 |
| Memory | Memory 사용량 \(M\) |
| Disk | Disk 용량 \(%\) |

**실시간 카운터**

실시간으로 수집된 카운터 정보에 대한 그래프를 5초 단위로 조회할 수 있습니다. 카운터 정보는 트랙잭션, 사용자, 자원으로 구분하여 조회할 수 있습니다. 실시간 카운터는 여러개의 그래프를 추가할 수 있어, 지표 별 비교가 가능하며, 시간 별 비교 또한 가능합니다. 지표 별 비교는 성능 문제에 대한 원인을 통합적으로 분석할 수 있습니다. 또한 지표들은 애플리케이션 서버 별 차이를 한 눈에 들어오도록 그래프를 표시하기에 애플리케이션 서버 별로 비교분석도 간단하게 할 수 있습니다. 실시간 카운터에서 조회할 수 있는 정보는 다음과 같습니다.Table 4. 트랜잭션

| 이름 | 설명 |
| :--- | :--- |
| TPS | 초당 트랜잭션 처리량 |
| 응답 시간 | 평균 트랜잭션 응답 시간 |
| 액티브 트랜잭션 | 평균 진행 중 트랜잭션 개수 |
| Sql 개수 | SQL 실행 개수 합 |
| Sql 에러 | SQL 에러 개수 합 |
| Sql 시간 | SQL 수행 시간 합 |
| Sql 페치 | SQL Fetch 개수 합 |
| Sql 페치 시간 | SQL Fetch 시간 합 |
| HttpC 개수 | Http Call 개수 합 |
| HttpC 에러 | Http Call 발생 에러 개수 합 |
| HTTP 요청 시간 | 아웃바운드 Http Call 시간 |

Table 5. 사용자

| 이름 | 설명 |
| :--- | :--- |
| Realtime user | 실시간 방문 사용자 |

Table 6. 자원

| 이름 | 설명 |
| :--- | :--- |
| CPU | CPU 사용량 \(Machin CPU\) |
| CPU sys | CPU System 사용량 \(%\) |
| CPU usr | CPU User 사용량 \(%\) |
| CPU wait | CPU Wait 총 합 |
| CPU Steal | Hypervisor 처리를 기다리느라 소비하는 시간 |
| CPU Irq | CPU가 하드웨어 인터럽트 처리를 위해 소비한 시간 총 합 |
| Process CPU | Process의 CPU 사용량 총 합 |
| Heap total | Heap total 량 \(M\) |
| Heap used | Heap used 량 \(M\) |
| Heap perm | Heap perm 량 \(M\) |
| Heap pending finalization | Pending finalization 개수 |
| GC count | GC Count 횟수 |
| GC time | GC 시간 총합 |
| Memory | Memory 사용량 \(M\) |
| Disk | Disk 용량 \(%\) |

**통계 분석**

과거 데이터를 기간별, 애플리케이션 서버별 등 원하는 조건을 설정하여 조회할 수 있습니다. 트랜잭션, 에러, SQL, 원격 HTTP 호출, 클라이언트 IP, 클라이언트 브라우저를 사용하여 과거 데이터를 통한 분석 및 튜닝이 가능합니다. 실시간 모니터링을 진행하지 못한 기간은 통계에서 제공하는 과거 데이터 조회를 통해 장애 및 성능 문제를 찾아낼 수 있습니다. 또한, 실시간 모니터링에서 발견하지 못하거나 프로파일 정보에서 발견하기 힘든 튜닝 포인트를 찾아낼 수 있으며 거시적인 문제의 추이 또한 그래프와 표를 통하여 파악할 수 있습니다.

**트랜잭션**

과거의 해당 기간동안 처리된 트랜잭션 정보를 조회할 수 있습니다.

* 조건부: 조회하고자 하는 날짜와, 시작시간, 기간을 선택하여 원하는 과거의 데이터를 조회할 수 있습니다. 애플리케이션 서버 전체, 개별 통계를 선택적으로 조회할 수 있습니다. 정렬 기준을 선택하여 정렬된 데이터를 조회할 수 있으며, 필터 기능을 통해 원하는 데이터를 선택적으로 데이터를 조회할 수 있습니다.

[![1030](https://github.com/jinronara/deleteme_2/raw/master/images/1030.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1030.png)

* 날짜 - 통계 조회 시작 날짜 설정
* 시작 시간 - 통계 조회 시작 시간 설정
* 기간 - 통계 조회 기간 설정 \(5분, 1시간, 3시간, 6시간, 12시간, 1일\)
* 애플리케이션 - 전체 또는 개별 애플리케이션 서버 설정
* Order by - 정렬 기준 설정

| 정렬 키 | 정렬 기준 |
| :--- | :--- |
| 수 | 트랜잭션 실행 건수 내림차순 |
| 에러 | 트랜잭션 에러 건수 내림차순 |
| 합계 시간 | 총 응답 시간 합 내림 차순 |
| 최대 시간 | 최대 트랜잭션 응답시간 내림차순 |
| 최소 시간 | 최소 트랜잭션 응답시간 오름차순 |
| 평균 시간 | 평균 트랜잭션 응답시간 내림차순 |
| 평균 CPU | 평균 트랜잭션 CPU |
| 메모리 평균 | 평균 트랜잭션 메모리 사용량 내림차순 |

* Filter - 필터링 기준 및 값 설정

| 필터링 키 | 필터링 기준 |
| :--- | :--- |
| 트랜잭션 | 트랜잭션 URL에 포함된 문자열 필터링 |

* 통계 결과

조회한 정보는 “컬럼 추가”를 통해 선택적으로 원하는 값을 추가/삭제 하여 볼 수 있습니다. 트랜잭션 통계에서는 다음과 같은 정보를 조회할 수 있습니다.[![1040](https://github.com/jinronara/deleteme_2/raw/master/images/1040.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1040.png)

* 트랜잭션 - 트랜잭션 서비스 URL
* 수 - 트랜잭션이 발생한 총 횟수 \(에러 횟수 포함\)
* 에러 - 트랜잭션 에러 카운트
* 평균시간 - 평균 응답시간 \(ms\)
* 합계시간 - 응답시간의 총 합\(ms\)
* 최소시간 - 최소 응답시간 \(ms\)
* 최대시간 - 최대 응답시간 \(ms\)
* 평균CPU
* 메모리 평균 - 평균 메모리 사용량
  * 활용처
* 과거의 특정 기간의 트랜잭션 발생 빈도를 확인할 수 있습니다.
* 응답시간이 느린 트랜잭션을 기간 별, 애플리케이션 서버 별로 찾아낼 수 있습니다.
* 평균 응답시간을 통하여 튜닝이 필요한 트랜잭션이나 애플리케이션 서버를 찾아낼 수 있습니다.

**에러**

과거의 해당 기간동안 발생한 정보를 조회할 수 있습니다. 한 눈에 해당 기간동안 발생한 에러를 조회할 수 있으며, 조건을 통해 원하는 에러만 찾을 수 있습니다. 모니터링을 하지 못한 상황에서는 가장 먼저 에러를 조회해야 하며, 에러가 났던 최초 시점부터 찾아가는 것이 좋습니다.

* 조건부: 조회하고자 하는 날짜와, 시작시간, 기간을 선택하여 원하는 과거의 데이터를 조회할 수 있습니다. 애플리케이션 전체 및 개별 통계를 선택적으로 조회할 수 있습니다. 필터 기능을 통해 찾고자하는 에러만을 조회할 수 있으며 에러 건수에 대한 내림차순으로 정보가 조회됩니다.
  * 날짜 - 통계 조회 시작 날짜 설정
  * 시작 시간 - 통계 조회 시작 시간 설정
  * 기간 - 통계 조회 기간 설정 \(5분, 1시간, 3시간, 6시간, 12시간, 1일\)
  * 애플리케이션 - 전체 또는 개별 애플리케이션 서버 설정
  * 필터 - 필터링 기준 및 값 설정

| 필터링 키 | 필터링 기준 |
| :--- | :--- |
| 클래스 | 에러 클래스에 포함된 문자열 필터링 |
| 메세지 | 에러 메세지에 포함된 문자열 필터링 |
| 트랜잭션 | 트랜잭션 URL에 포함된 문자열 필터링 |

* 통계 결과: 조회한 정보는 “컬럼 추가”을 통해 선택적으로 원하는 값을 추가/삭제 하여 볼 수 있습니다. 에러 통계에서는 다음과 같은 정보를 조회할 수 있습니다.
  * 클래스 - 에러 클래스
  * 트랜잭션 - 에러가 발생한 트랜잭션 URL
  * 메세지 - 에러 메시지
  * 시간 - 최초 에러 발생 시간
  * 수 - 에러 건수
* 활용처
  * 특정 기간의 에러 건수를 조회할 수 있습니다. 모니터링을 하고 있지 않았다면 가장 먼저 수행해야할 작업입니다.
  * 하루 단위의 조회를 통해 에러의 증감을 찾아낼 수 있습니다.
  * 과거 에러 데이터를 통해 새로운 에러 발생 여부를 알 수 있습니다.

**SQL**

과거의 해당 기간동안 실행한 SQL 정보를 조회할 수 있습니다. SQL의 실행이력과 함께 평균 실행시간 및 에러 건수등을 조회할 수 있습니다. SQL 수행시간, 페치 개수와 같은 정보는 SQL 튜닝에 있어 가장 중요하게 봐야할 부분입니다. 예를 들어, 과도한 Fetch 수 는 애플리케이션의 성능에 전체적인 영향을 미칠 수 있으며, 해당 트랜잭션에 응답시간을 느리게 만드는 원인이 됩니다.

* 조건부: 조회하고자 하는 날짜와, 시작시간, 기간을 선택하여 원하는 과거의 데이터를 조회할 수 있습니다. 애플리케이션 전체 및 개별 통계를 선택적으로 조회할 수 있습니다. 정렬 기준을 선택하여 데이터를 조회할 수 있으며, 필터 기능을 통해 원하는 데이터를 선택적으로 데이터를 조회할 수 있습니다.
  * 날짜 - 통계 조회 시작 날짜 설정
  * 시작 시간 - 통계 조회 시작 시간 설정
  * 기간 - 통계 조회 기간 설정 \(5분, 1시간, 3시간, 6시간, 12시간, 1일\)
  * 애플리케이션 - 전체 또는 개별 애플리케이션 서버 설정
  * 정렬 순서 - 정렬 기준 설정

| 정렬 키 | 정렬 기준 |
| :--- | :--- |
| 개수 | SQL 실행 건수 내림차순 |
| 에러 | SQL 에러 건수 내림차순 |
| 합계 시간 | SQL 수행시간의 합 내림차순 |
| 최소 시간 | 최소 SQL 수행 시간 오름차순 |
| 합계 시간 | 최대 SQL 수행 시간 내림차순 |
| 평균 시간 | 평균 SQL 수행 시간 내림차순 |
| 페치 개수 | SQL fetch 건수 내림차순 |

* Filter - 필터링 기준 및 값 설정

| 필터링 키 | 필터링 기준 |
| :--- | :--- |
| SQL | SQL 문에 포함된 문자열 필터링 |
| 데이터베이스 | Database connection url에 포함된 문자열 필터링 |

* 통계 결과: 조회한 정보는 “컬럼 추가”을 통해 선택적으로 원하는 값을 추가/삭제 하여 볼 수 있습니다. SQL 통계에서는 다음과 같은 정보를 조회할 수 있습니다.

| 이름 | 설명 |
| :--- | :--- |
| 데이터베이스 | Database connection url 주소 |
| SQL | 실행한 SQL 문 |
| 해시 | SQL 문의 hash 값 |
| 수 | SQL |
| 실행 건수 | 에러 |
| SQL 에러 건수 | 평균 시간 |
| SQL 평균 수행 시간 \(ms\) | 합계 시간 |
| SQL 총 수행 시간 \(ms\) | 최소 시간 |
| 최소 SQL 수행 시간 \(ms\) | 합계 시간 |
| 최대 SQL 수행 시간 \(ms\) | 페치 개수 |
| SQL fetch 건수 | 페치 시간 |

**원격 HTTP 호출**

과거의 해당 기간동안 실행한 외부 Http Call 정보를 조회할 수 있습니다. 외부 Http Call 실행 이력, 응답시간, 에러 정보를 조회할 수 있습니다.

* 조건부: 조회하고자 하는 날짜와, 시작시간, 기간을 선택하여 원하는 과거의 데이터를 조회할 수 있습니다. 애플리케이션 전체 및 개별 통계를 선택적으로 조회할 수 있습니다. 정렬 기준을 선택하여 데이터를 조회할 수 있으며, 필터 기능을 통해 원하는 데이터를 선택적으로 데이터를 조회할 수 있습니다.
  * 날짜 - 통계 조회 시작 날짜 설정
  * 시작 시간 - 통계 조회 시작 시간 설정
  * 기간 - 통계 조회 기간 설정 \(5분, 1시간, 3시간, 6시간, 12시간, 1일\)
  * 애플리케이션 - 전체 또는 개별 애플리케이션 서버 설정
  * 정렬 순서 - 정렬 기준 설정

| 정렬 키 | 정렬 기준 |
| :--- | :--- |
| 수 | Http call 실행 건수 내림차순 |
| 에러 | Http call 에러 건수 내림차순 |
| 합계 시간 | Http call 응답시간의 합 내림차순 |
| 최소 시간 | 최소 Http call 응답시간 오름차순 |
| 합계 시간 | 최대 Http call 응답시간 내림차순 |
| 평균 시간 | 평균 Http call 응답시간 내림차순 |

* Filter - 필터링 기준 및 값 설정

| 필터링 키 |
| :--- |
| 필터링 기준 |
| URL |
| Http call URL 주소에 포함된 문자열 필터링 |
| 호스트 |
| Http call을 보낸 Host의 IP에 포함된 문자열 필터링 |

* 통계 결과
  * 조회한 정보는 “컬럼 추가”를 통해 선택적으로 원하는 값을 추가/삭제 하여 볼 수 있습니다.

SQL 통계에서는 다음과 같은 정보를 조회할 수 있습니다.

| 이름 | 설명 |
| :--- | :--- |
| URL | Http call 을 요청한 url 주소 |
| 호스트 | Http call 을 요청한 Host 주소 |
| 포트 | Http call 을 요청한 포트 |
| 수 | Http call 실행 건수 |
| 에러 | Http call 에러 건수 |
| 평균 시간 | Http call 평균 응답시간 \(ms\) |
| 합계 시간 | Http call 총 응답시간 \(ms\) |
| 최소 시간 | 최소 Http call 응답시간 \(ms\) |
| 합계 시간 | 최대 Http call 응답시간 \(ms\) |

**클라이언트 IP**

과거의 해당 기간동안 접속한 사용자의 IP 통계 정보를 조회할 수 있습니다. IP 정보를 통해 사용자의 국가 및 도시를 확인 할 수 있으며, 이 정보를 통해 서비스 지역이 아닌 다른 지역에서 잘못된 접근이 발생하는지에 대한 여부를 판단할 수 있습니다. 또한, 방황벽 룰에 따른 특정 IP가 아닌 다른 IP에서 요청이 발생 했을 시 해킹의 위험이 있었는지에 대한 여부를 보실 수 있습니다.

* 조건부: 조회하고자 하는 날짜와, 시작시간, 기간을 선택하여 원하는 과거의 데이터를 조회할 수 있습니다. 애플리케이션 전체 및 개별 통계를 선택적으로 조회할 수 있습니다. 정렬 기준을 선택하여 데이터를 조회할 수 있으며, 필터 기능을 통해 원하는 데이터를 선택적으로 데이터를 조회할 수 있습니다.
  * 날짜 - 통계 조회 시작 날짜 설정
  * 시작 시간 - 통계 조회 시작 시간 설정
  * 기간 - 통계 조회 기간 설정 \(5분, 1시간, 3시간, 6시간, 12시간, 1일\)
  * 애플리케이션 - 전체 또는 개별 애플리케이션 서버 설정
  * Filter - 필터링 기준 및 값 설정

| 필터링 키 | 필터링 기준 |
| :--- | :--- |
| IP | 사용자 IP 주소에 포함된 문자열 필터링 |

* 통계 결과: 조회한 정보는“컬럼 추가을 통해 선택적으로 원하는 값을 추가/삭제 하여 볼 수 있습니다. 클라이언트 IP 통계에서는 다음과 같은 정보를 조회할 수 있습니다.

| 이름 | 설명 |
| :--- | :--- |
| IP | 클라이언트 IP 주소 |
| 국가 | IP 기반의 요청 국가 정보 |
| 도시 | IP 기반의 요청 도시 정보 |
| 수 | 요청 횟수 |

**클라이언트 브라우저**

과거의 해당 기간동안 접속한 사용자의 OS 및 브라우저 정보를 조회할 수 있습니다. 모바일 서비스의 경우 Android, iOS, Window 등 어떤 Device를 많이 사용하는지 판별할 수 있는 정보로 활용할 수 있습니다. 브라우저에 대한 정보 또한 관심있게 살펴보아야 할 우선 순위를 알 수 있습니다. 클라이언트 브라우저 통계는 BilevelChart 로 OS별 비중과 각각의 OS별 브라우저 사용 비중을 쉽게 파악할 수 있습니다. \* 조건부: 조회하고자 하는 날짜와, 시작시간, 기간을 선택하여 원하는 과거의 데이터를 조회할 수 있습니다. 애플리케이션 전체 및 개별 통계를 선택적으로 조회할 수 있습니다. 정렬 기준을 선택하여 데이터를 조회할 수 있으며, 필터 기능을 통해 원하는 데이터를 선택적으로 데이터를 조회할 수 있습니다. **날짜 - 통계 조회 시작 날짜 설정** 시작 시간 - 통계 조회 시작 시간 설정 \*\* 기간 - 통계 조회 기간 설정 \(5분, 1시간, 3시간, 6시간, 12시간, 1일\)

* 통계 결과: 조회한 정보는 “컬럼 추가”를 통해 선택적으로 원하는 값을 추가/삭제 하여 볼 수 있습니다. 클라이언트 IP 통계에서는 다음과 같은 정보를 조회할 수 있습니다.

| 이름 | 설명 |
| :--- | :--- |
| OS | 사용자 OS 이름 |
| 브라우저 | 사용자 접속 브라우저 이름 |
| 수 | 요청 횟수 |

**이벤트 기록**

과거의 해당 기간동안 발생한 여러 수준의 이벤트 정보를 조회할 수 있습니다. 치명적, 경고, 정보로 수준을 나누어서 이벤트를 조회할 수 있으며, 날짜 별, 애플리케이션 별로도 조회가 가능합니다.

* 조건부: 조회하고자 하는 날짜와, 시작시간, 기간을 선택하여 원하는 과거의 데이터를 조회할 수 있습니다. 애플리케이션 서버 전체, 개별 통계를 선택적으로 조회할 수 있습니다. 수준을 선택해 원하는 수준의 데이터를 선택적으로 데이터를 조회할 수 있습니다.

[![1050](https://github.com/jinronara/deleteme_2/raw/master/images/1050.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1050.png)

* 날짜 - 통계 조회 시작 날짜 설정
* 시작 시간 - 통계 조회 시작 시간 설정
* 기간 - 통계 조회 기간 설정 \(5분, 1시간, 3시간, 6시간, 12시간, 1일\)
* 애플리케이션 - 전체 또는 개별 애플리케이션 서버 설정
* 수준 - 필터링할 이벤트의 수준 설정

| 심각도 | 기준 |
| :--- | :--- |
| 치명적 | 서버 구동에 위험을 끼치는 정도 |
| 경고 | 서버 구동에 조금 장애가 되는 정도 |
| 정보 | 그 외 여러 정보 |

####  {#user-content-보고서}

#### 보고서 {#user-content-보고서}

하루의 종합적인 정보를 통해서 한눈에 파악 하기 쉽도록 도와주는 성능 데이터를 요약해서 보고서 형태로 제공해 드리고 있습니다.

**일일 보고서 \(전체 요약\)**

[![1060](https://github.com/jinronara/deleteme_2/raw/master/images/1060.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1060.png)

기본적으로는 달력에서 날짜를 선택해서 1일 보고서를 볼 수 있지만 세부적인 시간을 원한다면 해당 날짜의 원하는 시간을 설정 한 뒤 적용 버튼을 눌러 시간을 선택할 수 있습니다. 표현되고 있는 정보의 내용은 다음과 같습니다.

* 개요: 해당 기간 동안의 전체적인 정보를 나타냅니다.

| 이름 | 설명 |
| :--- | :--- |
| 방문자\(DAU\) | 사용자의 총합 |
| 요청 | 사용자의 요청 |
| 에러 | 에러가 일어난 비율 |
| 치명적 이벤트 | 사용자가 지정한 알림 범위에 도달하여 알림을 실행한 횟수 |
| 애플리케이션 서버 | 에이전트가 설치되어 모니터링 하고 있는 애플리케이션 서버의 총합 |
| CPU 코어 | 애플리케이션이 실행되고 있는 하드웨어의 CPU 코어의 총합 |

* 피크 타임 성능 요약 \(시간\): 해당 기간 동안중에서 가장 많은 요청이 들어온 시간대의 정보를 나타냅니다.

| 이름 | 설명 |
| :--- | :--- |
| TPS | Transaction per second |
| 방문자 | 사용자의 총합 |
| 요청 | 사용자의 요청 |
| 평균 응답 시간 | 평균 응답 시간 |
| 에러 | 에러가 일어난 비율 |
| 치명적 이벤트 | 사용자가 지정한 알림 범위에 도달하여 알림을 실행한 횟수 |
| 애플리케이션 서버 | 에이전트가 설치되어 모니터링 하고 있는 애플리케이션 서버의 총합 |
| CPU 코어 | 애플리케이션이 실행되고 있는 하드웨어의 CPU 코어의 총합 |

* Chart

| 이름 | 설명 |
| :--- | :--- |
| 실시간 사용자 | 사용자의 숫자 추이를 그래프로 표현 |
| TPS | 사용자의 요청을 그래프로 표현 |
| Hourly Visitors | 시간별 방문자들을 그래프로 표현 |
| 응답 시간 | 사용자가 요청한 Transaction을 처리한 응답시간의 추이를 그래프로 표현 |
| CPU | 애플리케이션이 실행되고 있는 하드웨어의 CPU사용량 추이를 그래프로 표현 |
| 애플리케이션 서버 | 에이전트가 설치되어 모니터링 하고 있는 애플리케이션의 추이를 그래프로 표현 |

* 애플리케이션 서버: 위의 보고서 통계들은 모든 정보를 통합해서 표현 한 것이라면 애플리케이션 서버는 각 서버별 데이터를 표현합니다.

| 이름 | 설명 |
| :--- | :--- |
| IP | 서버의 아이피 정보 |
| 요청 | 해당 서버에 들어온 사용자 요청 |
| 에러\(%\) | 사용자의 요청에 대한 응답 중에서 문제가 발생한 퍼센트 |
| 피크 타임 성능 요약 | 사용자가 설정한 기간 중에 모든 서버의 총 합을 기준으로 가장 높은 TPS를 기록한 순간 |

* ‘피크 타임 성능 요약’에서 출력하는 데이터

| 이름 | 설명 |
| :--- | :--- |
| 방문자 | 피크 타임에 해당 서버의 접속자 수 |
| TPS | 피크 타임에 해당 서버의 요청 수 |
| 응답시간 \(ms\) | 피크 타임에 해당 서버의 평균 응답시간 |
| 활동 중인 Trx | 피크 타임에 해당 서버에서 처리하고 있는 Transaction |

  ==== 일일 보고서 \(애플리케이션 요약\)[![1070](https://github.com/jinronara/deleteme_2/raw/master/images/1070.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1070.png)

기본적으로는 달력에서 날짜를 선택해서 1일 보고서를 볼 수 있지만 세부적인 시간을 원한다면 해당 날짜의 원하는 시간을 설정한 뒤 적용 버튼을 눌러 시간을 선택할 수 있습니다. 추가로 애플리케이션 탭에서 원하는 애플리케이션를 지정하여 해당하는 정보를 볼 수 있습니다. 출력되는 정보들은 다음과 같습니다.Table 7. Peak Time Info

| 이름 | 설명 |
| :--- | :--- |
| Peak Time | Peak Time |
| Respone Time | 응답 시간 |
| Respone Time user | 유저 응답 시간 |
| Active Account | 활성화 된 계정 |
| TPS | 피크 타임에 해당 서버의 요청 수 |
| Error \(%\) | 에러가 발생한 퍼센트 |

Table 8. Chart

| 이름 | 설명 |
| :--- | :--- |
| TPS | 사용자의 요청을 그래프로 표현 |
| RESPONSE TIME | 사용자가 요청한 Transaction을 처리한 응답시간의 추이를 그래프로 표현 |
| USER | 사용자의 숫자 추이를 그래프로 표현 |
| CPU | 애플리케이션이 실행되고 있는 하드웨어의 CPU사용량 추이를 그래프로 표현 |
| CPU \(MIN\) | CPU 사용량의 최소값을 그래프로 표현 |
| CPU \(MAX\) | CPU 사용량의 최대값을 그래프로 표현 |
| HEAP | 애플리케이션이 실행되고 있는 하드웨어의 Heap 메모리 사용량 추이를 그래프로 표현 |
| HEAP \(MIN\) | Heap 메모리 사용량의 최소값을 그래프로 표현 |
| HEAP \(MAX\) | Heap 메모리 사용량의 최소값을 그래프로 표현 |

* Transaction Top5
  * 트랜잭션 사용량 중 상위 5개를 표시
* Httpc Top5
  * 호출된 Http 중 상위 5개를 표시
* SQL Top5
  * 사용된 SQL 중 상위 5개를 표시   ==== 일일 보고서 \(애플리케이션 상세\)

[![1080](https://github.com/jinronara/deleteme_2/raw/master/images/1080.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1080.png)

특정 날짜의 특정 애플리케이션의 하루 동안의 데이터를 상세히 보여줍니다. 표시되는 목록들은 다음과 같습니다.

* 서비스 처리량
* 서비스 응답시간
* 서비스 사용자
* 응답분포도
* 애플리케이션 Top
  * 가장 느린 트랜잭션 Top 5
  * 많이 호출된 트랜잭션 Top 5
* 자원
  * CPU
  * Heap
* 기타
  * GC\_COUNT
  * GC\_TIME
  * DB\_CONNECTION\_ACTIVE
  * DB\_CONNECTION\_TOTAL
* 기타 자원
  * CPU\_MAX
  * CPU\_PROC
  * CPU\_STEAL
  * CPU\_IRQ
  * MEMORY   ==== 일일 피크타임 성능 비교

[![1090](https://github.com/jinronara/deleteme_2/raw/master/images/1090.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1090.png)

프로젝트에 존재하는 모든 애플리케이션 서버의 오늘, 어제, 지난주의 데이터를 보여줘 각 애플리케이션 별 비교 및 시간이 지남에 따른 변동폭을 보다 쉽게 파악할 수 있게 합니다.

**주간 보고서**

[![1100](https://github.com/jinronara/deleteme_2/raw/master/images/1100.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1100.png)Figure 2. 주간보고서[![1110](https://github.com/jinronara/deleteme_2/raw/master/images/1110.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1110.png)Figure 3. 월간보고서

기본적으로 달력에서 날짜를 선택하고, 선택한 날짜부터 7일간의 주간 보고서를 볼 수 있습니다. 표현되고 있는 정보의 내용은 다음과 같습니다.

| 이름 | 설명 |
| :--- | :--- |
| 가동률 | 서버가 가동되고 있는 시간\(%\) |
| 일일 방문자 | 하루간 방문한 누적 방문자 수 |
| 일일 트랜잭션 수 | 하루간 처리한 누적 트랜잭션의 수 |
| 액티브 트랜잭션 | 단위 시간당 평균 처리중 트랜잭션의 수 |
| 실시간 사용자 | 단위 시간당 평균 실시간 사용자 수 |
| 트랜잭션/초\(TPS\) | 단위 시간당 처리된 평균 초당 트랜잭션 |
| 응답시간 | 단위 시간당 평균 응답시간 |
| CPU | 단위 시간당 평균 CPU 사용량 |
| 힙 | 단위 시간당 평균 힙 메모리 사용량 |

**월간 보고서**

기본적으로 달력에서 날짜를 선택하고, 선택한 날짜부터 한달간의 월간 보고서를 볼 수 있습니다.

ex\) 7월 23일을 선택 시 8월 22일 까지 표현되고 있는 정보의 내용은 다음과 같습니다.

| 이름 | 설명 |
| :--- | :--- |
| 고객 충성도\(DAU, WAU\) | 재방문한 방문자의 비율 |
| 일일 방문자\(DAU\) | 하루간 방문한 누적 방문자 수 |
| 일일 트랜잭션 수 | 하루간 처리한 누적 트랜잭션의 수 |
| 시간당 트랜잭션 개수 | 한 시간 동안 처리한 누적 트랜잭션의 수 |
| 시간당 트랜잭션 | 에러 개수 한 시간 동안 트랜잭션에서 발생한 누적 에러의 수 |
| 액티브 트랜잭션 | 단위 시간당 평균 처리 중 트랜잭션의 수 |
| 트랜잭션/초\(TPS\) | 단위 시간당 처리된 평균 초당 트랜잭션 |
| 시간당 평균 응답 시간 | 한 시간 동안 평균 응답 시간 |



#### 에이전트 관리 {#user-content-에이전트-관리}

와탭 APM 모니터링 서비스는 서버 메뉴를 통해 JVM의 프로파일 정보를 제공하여, 애플리케이션 서버 관리를 위한 다양한 정보를 제공합니다.

**에이전트 목록**

서버 메뉴에 최초 진입 시 프로젝트에서 입수한 에이전트가 설치된 애플리케이션 서버로부터의 전송 정보를 기준으로 등록된 애플리케이션 서버 목록이 표시됩니다.[![1120](https://github.com/jinronara/deleteme_2/raw/master/images/1120.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1120.png)

* 표시 항목

| 항목 | 설명 |
| :--- | :--- |
| 애플리케이션 | 애플리케이션 서버 식별 용도의 명칭 |
| 시작 시간 | 애플리케이션 서버 기동 시각 |
| 활성/비활성 | 에이전트의 최종 활성/비활성 상태 천이 시각 |
| 상태 | 에이전트의 활성/비활성 여부 \(active 또는 inactive로 표시\) |
| 버전 | 에이전트 버전 |
| IP | 애플리케이션 서버의 네트워크 인터페이스 IP 주소 |
| CPU 코어 | 물리 서버의 코어 수 |

* 애플리케이션 기본 패턴
  * {애플리케이션 서버 유형}-{IP주소의 3번째 수}-{IP주소의 4번째 수}-{서비스 포트}
* 정보 : 더보기 버튼 클릭 시 하위 버튼을 통해 추가 기능 제공

| 기능 | 설명 |
| :--- | :--- |
| 부트 환경 | 에이전트 기동 옵션 정보 |
| 환경 | 시스템 환경변수 정보 |
| 컴포넌트 버전 | 로딩된 jar 라이브러리의 버전 정보 |
| 스레드 목록 | 실행 중 쓰레드 현황 |
| 힙 히스토그램 | Heap 점유 객체 현황 |
| 로드된 클래스 | 로딩된 클래스 현황 |
| 오픈 소켓 | 아웃바운드 소켓 활용 정보 |
| 설정 | 에이전트 옵션 변경 |
| 시스템 GC | 명시적 GC 수행 |

**실행 환경 확인**

**실행 환경 변수**

{text 내용 추가 필요}

**시스템 환경 변수**

{text 내용 추가 필요}

**라이브러리 목록**

{text 내용 추가 필요}

**런타임 정보 확인**

{text 내용 추가 필요}

**실행 중 쓰레드**

스레드 목록은 실행 중 쓰레드 현황을 표시합니다.

| 이름 | 설명 |
| :--- | :--- |
| 표시 항목 |  |
| 스택 | 스택 정 |
| 아이디 | 쓰레드 ID |
| 상태 | 쓰레드 상태 |
| 이름 | 쓰레드 명 |
| CPU | CPU 총 사용시간\(ms\) |
| 차이 |  |

**메모리 점유객체**

{text 내용 추가 필요}

**로딩된 클래스**

로드된 클래스는 애플리케이션 서버에 로딩된 클래스 현황을 제시합니다. ClassNotFoundException/NoClassDefFoundError와 같이 클래스 로딩과 관련된 예외 상황 발생 시 문제 유발 클래스가 로딩이 안 된 상태이거나 중복 로딩되었을 경우 본 화면의 정보를 통해 확인 할 수 있습니다.[![1130](https://github.com/jinronara/deleteme_2/raw/master/images/1130.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1130.png)

* 표시 항목

| 이름 | 설명 |
| :--- | :--- |
| 번호 |  |
| 이름 | 클래스 Full Path |
| 유형 | 클래스 타입 \(C: class / I: Interface\) |
| SUPERCLASS | 상위 클래스 |
| 인터페이스 |  |
| 자원 | 클래스 파일 경로 |

* 이미 로딩된 클래스를 재정의 하기 위한 팝업을 표시 : 실행 중인 애플리케이션 서버에 Java Attach 방식으로 와탭을 설치한 경우, 애플리케이션 서버가 제공하는 일부 모듈의 경우 바이트코드 변환이 적용되지 않아 모니터링 기능이 적용되지 않을 수 있습니다. 이러한 경우 클래스 재정의를 통해 바이트코드 변환을 유도 할 수 있습니다. 에이전트의 plugin 기능을 활용하는 경우에도, 애플리케이션 서버가 기동 된 상태에서 적용 할 경우, 플러그인이 적용될 대상 클래스를 재정의 하여 적용 할 수 있습니다.

[![1140](https://github.com/jinronara/deleteme_2/raw/master/images/1140.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1140.png)

* 클래스 시그니처 확인: 클래스 로딩 현황의 클래스 및 인터페이스를 클릭하면 클래스 시그니처를 확인 할 수 있습니다.

[![1150](https://github.com/jinronara/deleteme_2/raw/master/images/1150.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1150.png)

**소켓 오픈 집계**

오픈 소켓은 애플리케이션 서버 실행 이후 아웃바운드 호출용으로 Open 되었던 Socket의 누적 정보를 제공합니다.

* 표시 항목

| 이름 | 설명 |
| :--- | :--- |
| 키 | 랜덤하게 생성된 난수 키 |
| 호스트 | 아웃바운드 소켓 접속 대상 호스트 IP 주소 |
| 포트 | 아웃바운드 소켓 접속 대상 포트 |
| 수 | 애플리케이션 소켓 접속 대상 포트 |
| 서비스 | 호출 서비스 URL |

[![1160](https://github.com/jinronara/deleteme_2/raw/master/images/1160.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1160.png)

**시스템 GC**

**에이전트 설정**

{text 내용 추가 필요}

### 인프라 모니터링 {#user-content-인프라-모니터링}

#### 관리 {#user-content-관리-1}

와탭 Infra 모니터링 서비스는 다수의 서버를 프로젝트로 그룹화 하여 관리합니다.[![1170](https://github.com/jinronara/deleteme_2/raw/master/images/1170.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1170.png)

**에이전트 설치**

[![1180](https://github.com/jinronara/deleteme_2/raw/master/images/1180.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1180.png)

와탭 콘솔의 프로젝트 그룹에서 추가 버튼을 누릅니다.[![1190](https://github.com/jinronara/deleteme_2/raw/master/images/1190.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1190.png)

INFRA STRUCTURE 아이콘 선택 후 각 입력란에 해당하는 정보를 입력하고 전송 버튼을 눌러 프로젝트를 추가합니다.

**Linux**

새롭게 생성한 인프라 모니터링 프로젝트를 클릭하여 아래와 같은 에이전트 설치 화면에 진입합니다.

* 해당 화면은 프로젝트 관리 → 에이전트 설치 부분에서 확인 가능합니다.

[![1200](https://github.com/jinronara/deleteme_2/raw/master/images/1200.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1200.png)

**패키지 저장소\(Repository\) 추가**

에이전트 설치 페이지에서 상위에 위치한 OS탭에서 서버 OS와 동일한 탭을 클릭합니다.

설치 페이지에 존재하는 “와탭 저장소\(Repository\)를 추가합니다.”의 밑에 있는 명령어를 copy 버튼을 눌러 복사하거나 밑의 명령어를 설치하고자 하는 서버에 입력합니다.Debian / Ubuntu

```text
$ wget http://repo.whatap.io/debian/release.gpg -O -|sudo apt-key add -
$ wget http://repo.whatap.io/debian/whatap-repo_1.0_all.deb
$ sudo dpkg -i whatap-repo_1.0_all.deb
$ sudo apt-get update
```

CentOS / Amazon Linux

```text
$ sudo rpm --import http://repo.whatap.io/centos/release.gpg
$ sudo rpm -Uvh http://repo.whatap.io/centos/5/noarch/whatap-repo-1.0-1.noarch.rpm
```

**에이전트 설치**

설치 페이지에 존재하는 “서버 모니터 패키지를 설치하십시오.” 밑에 있는 명령어를 copy 버튼을 눌러 복사하거나 밑의 명령어를 설치하고자 하는 서버에 입력합니다.Debian / Ubuntu

```text
$ sudo apt-get install whatap-infra
```

CentOS / Amazon Linux

```text
$ sudo yum install whatap-infra
```

**라이선스 등록**

설치 페이지에 존재하는 “설정 스크립트를 실행하여 서버 모니터 데몬을 시작하십시오.” 밑에 있는 박스를 클릭하여 라이선스를 발급받습니다. 이후 생성되는 명령어를 copy 버튼을 눌러 복사하거나 아래의 명령어에 라이선스키와 서버 IP를 추가하여 설치하고자 하는 서버에 입력합니다.

```text
$ echo "license=[발급된 라이선스키]" |sudo tee /usr/whatap/infra/conf/whatap.conf
$ echo "whatap.server.host=[할당된 와탭 서버 IP]" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
$ echo "createdtime=`date +%s%N`" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
$ sudo service whatap-infra restart
```

* 설치 페이지에서 발급받은 명령어에는 라이선스 키와 IP가 입력되어 있습니다.
* 데이터 전송을 위해 6600 PORT가 열려 있어야 합니다. \(TCP 아웃바운드\)

**Windows**

새롭게 생성한 인프라 모니터링 프로젝트를 클릭하여 아래와 같은 에이전트 설치 화면에 진입합니다.

* 해당 화면은 프로젝트 관리 → 에이전트 설치 부분에서 확인 가능합니다.

[![1210](https://github.com/jinronara/deleteme_2/raw/master/images/1210.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1210.png)

**에이전트 파일 다운로드**

에이전트 설치 페이지 상단에 위치한 OS 탭에서 Windows를 클릭합니다. 이후 Whatap\_infra.exe 를 클릭하여 설치파일을 다운로드 합니다.

* 보안상 .exe 형식의 파일이 받아지지 않는 사용자를 위하여 .zip 형식의 파일도 제공됩니다.
* 보안을 위해 브라우저를 통한 직접 설치보단 다운로드 받은 파일 실행을 권장합니다.

**에이전트 파일 업로드**

다운로드 받은 인프라 에이전트 설치파일을 설치하고자 하는 서버에 접속하여 업로드 합니다.

**라이선스 발급**

설치 페이지에서 라이선스 키와 IP를 발급받습니다.[![1220](https://github.com/jinronara/deleteme_2/raw/master/images/1220.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1220.png)

**에이전트 설치**

서버에서 업로드 받은 인프라 에이전트 설치파일을 실행합니다.

실행 시 다음과 같은 화면을 볼 수 있습니다. 입력란에 발급받은 라이선스 키와 IP를 입력하고 진행합니다.[![1230](https://github.com/jinronara/deleteme_2/raw/master/images/1230.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1230.png)

정상적으로 설치가 완료된 경우 다음과 같은 화면을 볼 수 있으며, 에이전트가 자동적으로 모니터링을 시작합니다. 완료 버튼을 눌러 설치를 완료합니다.[![1240](https://github.com/jinronara/deleteme_2/raw/master/images/1240.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1240.png)

* 데이터 전송을 위하여 6600 PORT가 열려 있어야 합니다. \(TCP 아웃바운드\)

**프로젝트 관리**

**사용자 관리**

프로젝트를 생성하였거나 SuperAdmin 권한을 이전 받았을 경우 프로젝트 설정에서 해당 프로젝트의 기본 정보\(이름, 알림 표시 시간대, API토큰\) 입력/수정 및 사용자 초대를 통하여 서버 모니터링 현황을 공유할 수 있습니다.[![1250](https://github.com/jinronara/deleteme_2/raw/master/images/1250.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1250.png)

| 이름 | 설명 |
| :--- | :--- |
| 프로젝트 명 | 프로젝트 생성시에 기입한 이름이 들어갑니다. Edit 버튼을 눌러 프로젝트 이름을 변경할 수 있습니다. |
| 애플리케이션 시간대 | 알림 발생시 메일/SMS에 표시되는 시간을 지정할 수 있습니다. 원하는 시간대를 선택한 뒤 Edit버튼을 눌러 이후 발생하는 알림의 표시 시간을 변경할 수 있습니다. |
| 라이선스 키 | 각각의 프로젝트별로 발급되는 라이선스 키입니다. |
| 프로젝트 지역 | 프로젝트에 속한 서버에서 발생하는 데이터를 저장하는 수집 서버의 위치입니다. |
| Api 토큰 | Open API를 사용할 시 사용자를 식별 및 인증하는 문자열입니다. |
| 액티브 회원 | 해당 프로젝트에 등록된 사용자 명단입니다. SuperAdmin 계정의 경우 타 계정의 권한을 변경/삭제할 수 있습니다 |

* 주의: Api 토큰은 노출되지 않도록 사용자가 주의하여 관리하여야 하며, 노출 의심 시 재발급 버튼을 눌러 갱신할 수 있습니다.

**알림 설정**

**알림 설정 개요**

서버 임계 상황에서 알림이 발생 시 Email / SMS / Mobile App으로 알림을 수신할 수 있게 됩니다. 알림 메시지 언어 설정 및 미디어 별 수신 여부 / 수신 시간 / 수신 요일 등을 설정할 수 있습니다.[![1260](https://github.com/jinronara/deleteme_2/raw/master/images/1260.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1260.png)

| 이름 | 설명 |
| :--- | :--- |
| 알림 언어 | 알림을 받을 언어를 설정할 수 있습니다. |
| 알림 시간 | 설정한 시간에만 알림이 옵니다. |
| 알림 요일 | 설정한 요일에만 알림이 옵니다. |

**이메일 알림 설정**

알림이 발생한 경우 해당 프로젝트에 등록된 이메일로 알림 메일이 발송됩니다. 만약 알림을 받고 싶지 않은 경우 “이메일로 알림을 받겠습니다.”의 체크를 해제해주시면 됩니다.

**문자 알림 설정**

알림이 발생한 경우 해당 프로젝트에 등록된 휴대폰 번호로 알림 메시지가 발송됩니다. 만약 알림을 받고 싶지 않은 경우 “문자로 알림을 받겠습니다.”의 체크를 해제해주시면 됩니다.

* SMS 알림 기능은 유료 서버에 한정됩니다.

**모바일 알림 설정**

알림이 발생한 경우 해당 프로젝트에 등록된 모바일 APP으로 알림이 발송됩니다. 만약 알림을 받고 싶지 않은 경우 “모바일로 알림을 받겠습니다.”의 체크를 해제해주시면 됩니다.

**모바일 앱 설치**

Google Play Store, App Store에서 WhaTap을 검색하여 설치합니다.[![1270](https://github.com/jinronara/deleteme_2/raw/master/images/1270.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1270.png)

**모바일 앱 활용**

[![1280](https://github.com/jinronara/deleteme_2/raw/master/images/1280.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1280.png)[![1290](https://github.com/jinronara/deleteme_2/raw/master/images/1290.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1290.png)[![1300](https://github.com/jinronara/deleteme_2/raw/master/images/1300.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1300.png)

**다운 체크 설정**

**다운 체크 개요**

같은 내부 네트워크에 존재하는 서버들이 서로의 포트 작동 여부를 확인하여 수집 서버로 전송합니다. 해당 방식은 가용성 기능을 사용할 때 모니터링 서버와 수집 서버간 네트워크 문제로 인하여 발생하는 오탐을 줄이기 위하여 내부 서버 서로 감시를 하여 서버의 다운 여부를 확인하여 수집 서버로 전송합니다.[![1310](https://github.com/jinronara/deleteme_2/raw/master/images/1310.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1310.png)

* 탐지 역할을 하는 서버를 선택할 수 있습니다. 클릭 시 드롭다운 메뉴가 나와 현재 서버 목록을 보여줍니다.
* 탐지할 서버를 추가할 수 있습니다.
* 현재 탐지되는 서버의 이름, IP, 포트에 대한 정보를 목록으로 보여줍니다.
* 등록 된 서버를 수정 / 삭제할 수 있습니다.

**다운 체크 설정**

다운 체크 설정 화면에서 추가 혹은 EDIT 버튼을 클릭 시 설정창이 발생합니다.[![1320](https://github.com/jinronara/deleteme_2/raw/master/images/1320.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1320.png)

| 이름 | 설명 |
| :--- | :--- |
| 이름 | 클릭시 드롭다운 메뉴가 인프라에 등록된 서버 목록을 보여줍니다. |
| IP | 드롭다운으로 서버를 선택시 자동으로 IP가 추가됩니다. |
| Port | 탐지역할 서버가 확인할 포트를 입력합니다. |
| SSH | RDP Port를 포함한 서버가 작동하면 반드시 접속가능한 Port를 입력하실 수 있습니다. |

#### 실시간 모니터링 {#user-content-실시간-모니터링-1}

**서버 목록**

[![1330](https://github.com/jinronara/deleteme_2/raw/master/images/1330.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1330.png)

1. 등록된 전체 서버들의 상태를 한 눈에 볼 수 있습니다.
2. 일시정지 / 재개 / 해지 하거나 비교하기 위해 서버\(들\)를 선택할 수 있습니다.
3. 서버에 대한 요약 차트를 볼 수 있습니다.
4. 등록된 서버명입니다. 클릭 시 개별 서버에 대한 상세 정보를 확인할 수 있습니다.
5. 선택된 서버들을 한번에 비교하여 볼 수 있습니다.
6. 원하는 서버에 태그를 만들어 해당 태그로 취사 선택하여 확인할 수 있습니다.
7. 등록된 서버들에 대한 정보를 취사 선택하여 확인할 수 있습니다. 컬럼에는 다음과 같은 정보들을 확인할 수 있습니다. 컬럼 및 컬럼 정렬 상태는 저장되어 다음에 접속하였을 때도 계속 유지됩니다.
8. 모니터링 서버를 일시정지 / 재개 / 해지할 수 있습니다.
   * 주의: 해당 기능은 프로젝트의 SuperAdmin과 Admin만 사용할 수 있습니다.
9. 새로운 서버를 등록할 수 있습니다.
10. 서버를 검색할 수 있습니다. 서버 이름, IP를 포함한 키워드를 입력하여 목록에서 원하는 서버만을 볼 수 있습니다.

**컬럼 데이터**

| 이름 | 설명 |
| :--- | :--- |
| Server Name | 등록된 서버의 Display Name. 서버 상세정보 화면에서 변경할 수 있습니다. |
| OS | 등록된 서버의 운영체제 환경 |
| IP \(Public + Private\) | 외부/내부망 IP 모두 표시 |
| Public IP | 외부망 IP |
| Private IP | 내부망 IP |
| CPU | CPU 사용량\(%\) |
| Memory | Memory 사용량\(%\) |
| Disk\(all\) | 마운드 되어 있는 전체 디스크 현황 |
| Disk\(max\) | 최대 사용량 디스크 현황 |
| Network\(all\) | 연결되어 있는 전체 네트워크 어댑터 현황 |
| Network\(max\) | 최대 사용률 네트워크 현황 |
| CPU Vendor | 가용중인 CPU명 |
| RAM | 메모리 총량 |
| Up Time\(days\) | 서버가 켜진 후 경과한 일수 |
| DISK IO%\(all\) | 디스크 장치들의 사용 시간을 백분율 한 것 전부 출력 |
| DISK IO%\(max\) | 디스크 장치들의 사용 시간을 백분율 한 것 중 최대값 출력 |
| DISK IOPS\(all\) | 디스크 장치들의 IO 초당 사용 횟수를 전부 출력 |
| DISK IOPS\(max\) | 디스크 장치들의 IO 초당 사용 횟수 중 최대값 출력 |
| DISK BPS%\(all\) | 디스크 장치가 IO에 사용한 대역폭 전부 출력 |
| DISK BPS%\(max\) | 디스크 장치가 IO에 사용한 대역폭 중 최대값 출력 |

**서버 상세 정보**

**상세 정보 개요**

[![1340](https://github.com/jinronara/deleteme_2/raw/master/images/1340.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1340.png)

| 번호 | 이름 | 설명 |
| :--- | :--- | :--- |
| 1 | 운영 체제 | OS 사용 정보 |
| 2 | CPU Usage | CPU 사용량 정보 |
| 3 | Memory Usage | Memory 사용량 정보 |
| 4 | Network | 네트워크 현황 정보 |
| 5 | Disk I/O | Disk I/O 수치 정보 |
| 6 | Server Info | 해당 서버의 운영체제, 화면 명, IP 주소, 와탭 에이전트 정보 |
| 7 | 조회 기간 | 화면상에 보여줄 데이터의 조회 기간을 변경할 수 있습니다. |
| 8 | Process | 해당 서버 내에 돌아가고 있는 프로세스의 리소스 정보 |
| 9 | Alert List | 등록된 서버 내에서 발생했던 최근 알림 기록 |

* CPU / Memory / Network / Disk IO의 경우 우측 See details를 통해 자세한 정보를 확인할 수 있습니다.

조회 기간 상세 설명

* 기본 설정: Real time으로 30분전부터 현재까지의 데이터. 기본 설정으로 세팅되어 있는 경우 5초마다 차트가 흐르며 실시간으로 모니터링이 가능합니다. 각각의 차트 우측에 돌아가고 있는 애니메이션이 활성화가 됩니다.
* 시간값 좌측의 화살표를 클릭하면 선택된 기간만큼의 앞, 혹은 뒤로 이동하며 차트를 조회합니다. 조회 기간 이동 시 선택 된 기간과 관계 없이 Real time 기능은 비활성화 됩니다.
* 가장 좌측에 있는 화살표를 클릭하면 현재 시간으로 돌아갑니다.
* 조회 기간마다 다른 차트 시간 간격을 갖습니다.
  * 30분, 1시간: 5초
  * 3시간, 12시간, 24시간: 5분
  * 7일, 30일: 1시간

**CPU 상세 정보**

서버 상세 정보의 CPU Usage 우측 See Details를 통하여 상세 페이지로 들어올 수 있습니다.[![1350](https://github.com/jinronara/deleteme_2/raw/master/images/1350.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1350.png)

| 이름 | 설명 | 단위 |
| :--- | :--- | :--- |
| CPU Usage | CPU 사용량 | % |
| CPU Idle | CPU 미 사용량 | % |
| CPU I/O Wait | CPU가 디스크 IO가 완료되는 것을 기다리느라 소비하는 시간 | % |
| CPU Steal | 가상 CPU가 실제 CPU 시간을 기다리느라 소비하는 시간 | % |
| CPU IRQ | CPU가 하드웨어 인터럽트 처리를 위해 소비한 시간 | % |
| CPU SOFTIRQ | CPU가 소프트웨어 인터럽트 처리를 위해 소비한 시간 | % |
| CPU Load | 1분, 5분, 15분 동안 평균적으로 대기하고 있는 프로세스의 수 | 개수 |

**메모리 상세 정보**

서버 상세 정보의 Memory Usage 우측 See Details를 통해 상세 페이지로 들어올 수 있습니다.[![1360](https://github.com/jinronara/deleteme_2/raw/master/images/1360.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1360.png)

| 이름 | 설명 | 단위 |
| :--- | :--- | :--- |
| Memory Usage | Windows: Total Memory - Available Memory Linux: Total Memory - \(buffer + cache + free\) CentOS7: 100 - Memory Available | %, Byte |
| Memory Free | Windows: Available Memory Linux: Process가 사용가능한 메모리 중 buffer, cache를 제외한 용량 CentOS7 계열: SWAP 증가 없이 프로세스가 사용할 수 있는 메모리 | % |
| Memory Available | Windows: 시스템 상에서 사용 가능한 메모리 Linux: 사용 가능한 메모리 CentOS: SWAP 증가 없이 프로세스가 사용할 수 있는 메모리 | % |
| Memory Swap Used | Swap 영역 사용량 | %, Byte |
| Memory Page Faults | 메모리 공간에 존재하지 않는 코드나 데이터를 요청 시 발생하는 Soft Page Fault+Hard Page Fault | 개수 |

**네트워크 상세 정보**

서버 상세 정보의 Network 우측 See Details를 통해 상세 페이지로 들어올 수 있습니다.[![1370](https://github.com/jinronara/deleteme_2/raw/master/images/1370.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1370.png)

| 번호 | 이름 | 설명 | 단위 |
| :--- | :--- | :--- | :--- |
| 1 | Network Adapter | 연결된 네트워크 어댑터별 상세 정보 |  |
| 2 | Traffic In/Out | Network Interface가 송/수신한 트래픽 대역폭 | bps |
| 3 | Packet In/Out | Network Interface가 송/수신한 패킷 대역폭 | ps |
| 4 | Error In/Out | Network Interface에서 발생한 송/수신 전송 오류 | ps |
| 5 | Dropped In/Out | Network Interface에서 발생한 송/수신 중 처리하지 못하고 timeout이 발생하여 손실 처리된 것 | ps |

**디스크 상세 정보**

서버 상세 정보의 Disk I/O 우측 See Details를 통해 상세 페이지로 들어올 수 있습니다.[![1380](https://github.com/jinronara/deleteme_2/raw/master/images/1380.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1380.png)

| 번호 | 이름 | 설명 | 단위 |
| :--- | :--- | :--- | :--- |
| 1 | Disk | 마운트 된 디스크별 상세 정보 |  |
| 2 | Disk I/O | 디스크 장치가 사용중인 시간 | % |
| 3 | IOPS | Read/Write 디스크 장치가 IO를 사용한 초당 횟수 | ps |
| 4 | Disk Bps Read/Write | 디스크 장치가 IO에 사용한 대역폭 | bps |
| 5 | Used Space | 파일 시스템 사용 용량 | %, Byte |
| 6 | Free Space | 사용할 수 있는 파일 시스템 용량 | %, Byte |
| 7 | Queue Length | 대기중인 I/O 요청 수 | 개수 |

7.2.2.2.6. 프로세스 상세 정보[![1390](https://github.com/jinronara/deleteme_2/raw/master/images/1390.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1390.png)

1. 정렬 기준: 프로세스들의 정렬 기준 및 개수를 결정할 수 있습니다. CPU / Memory / Name / IO / Count를 기준으로 정렬할 수 있습니다.

[![1400](https://github.com/jinronara/deleteme_2/raw/master/images/1400.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1400.png)

1. 알림 정책 설정: 개별 프로세스에 대해 Alert 정책을 설정할 수 있습니다. 자세한 내용은 프로세스 알림 정책을 참고하시길 바랍니다.
2. 프로세스 세부 정보: 해당 프로세스 클릭 시 프로세스에 대한 세부정보를 볼 수 있습니다. 자세한 내용은 개별 프로세스 정보를 참고하시길 바랍니다.
3. 더 보기: 현재 화면상에 보이지 않는 프로세스들 역시 확인할 수 있습니다.

**개별 프로세스 정보**

각각의 프로세스를 클릭할 경우 개별 프로세스 정보를 확인할 수 있습니다.[![1410](https://github.com/jinronara/deleteme_2/raw/master/images/1410.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1410.png)

| 번호 | 이름 | 설명 | 단위 |
| :--- | :--- | :--- | :--- |
| 1 | 프로세스 개요 | \* PID, 프로세스명, CPU/Memory/RSS 사용률 및 사용자 권한을 확인 \* 해당 프로세스가 한 개 이상 실행될 경우 추가적으로 리스트업 \* RSS: 메모리 내부에서 프로세스가 차지하는 메모리의 양 |  |
| 2 | CPU Used\(%\) | 프로세스가 사용한 CPU 시간의 백분율 | % |
| 3 | Memory Used\(%\) | 프로세스가 사용한 메모리 비율 | % |
| 4 | I/O Used \(Bps\) | Windows: File, Network, Device로부터 발생한 IO 대역폭 | bps |
| 5 | IP Used \(Count\) | 같은 이름의 프로세스에서 사용 중인 Listen Port 및 연결 개수 | count |
| 6 | File Used \(Byte\) | 같은 이름의 프로세스에서 Open한 파일 이름과 크기 | byte |

#### 대시보드 {#user-content-대시보드}

**Compound Eye**

**Compound Eye 개요**

Compound Eye는 사용자들에게 와탭 에이전트가 설치된 모든 서버들을 빈틈없이 볼 수 있게 해줍니다.[![1420](https://github.com/jinronara/deleteme_2/raw/master/images/1420.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1420.png)[![1430](https://github.com/jinronara/deleteme_2/raw/master/images/1430.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1430.png)

하나의 눈\(Eye\) 입니다. 총 5가지의 정보를 제공합니다.

* CPU 사용량
* Memory 사용량
* Disk 사용량
* 네트워크의 Rx \(수신량\)
* 네트워크의 Tx \(송신량\)
  * 특히 네트워크 사용량에서 Rx/Tx 를 추가함으로 DDoS와 같이 외부 공격이 여러 서버에서 일제히 발생하는지 확인할 수 있습니다.

[![1440](https://github.com/jinronara/deleteme_2/raw/master/images/1440.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1440.png)

서버에 이상 현상이 발생한 경우 개별 아이\(Eye, 눈\)는 색상으로 그 상태를 표현합니다.

* 서버 모니터링이 일시정지 된 상태입니다. 회색으로 표현됩니다.
* 서버가 경고 상태입니다. 주황색으로 표현됩니다.
* 서버가 위험 상태입니다. 빨간색으로 표현됩니다.

추가적으로 서버 위에 마우스를 위치하게 될 경우 개별 정보가 수치화 된 팝업 메시지가 뜨게 되며, 서버 클릭 시 해당 서버의 요약 페이지로 이동하게 되어 서버에 대한 더욱 자세한 내용들을 파악할 수 있습니다.

**Traffic Max Value 옵션**

네트워크 환경에 따라 트래픽 양이 변화할 수 있기 때문에 트래픽의 최대값을 조정할 수 있습니다. 희망하는 트래픽 최대값을 설정하면 값에 따라 Rx/Tx 그래프가 변경됩니다.[![1450](https://github.com/jinronara/deleteme_2/raw/master/images/1450.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1450.png)

**가용성**

가용성 기능은 여러 서버들의 서버 상태 기록을 그래프로 보여 한눈에 파악할 수 있도록 합니다.[![1460](https://github.com/jinronara/deleteme_2/raw/master/images/1460.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1460.png)

가용성 차트는 다운 체크에서 추가한 IP들의 가용성 차트를 표시합니다. 기본으로 오늘 날짜의 00:00부터 현재까지의 가용성 차트를 표시합니다. 1일, 7일, 30일 등 범위를 지정할 수 있으며 화살표 클릭으로 차트의 날짜를 변경할 수 있습니다.

#### 알림 정책 {#user-content-알림-정책}

**알림 정책 설정**

**알림 정책 개요**

서버 및 프로세스 알림 정책을 생성, 수정, 삭제할 수 있습니다.[![1470](https://github.com/jinronara/deleteme_2/raw/master/images/1470.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1470.png)

| 이름 | 설명 |
| :--- | :--- |
| 추가 | 해당 정책을 추가할 수 있습니다. |
| COPY | 다른 인프라에 해당 정책을 복사할 수 있습니다. |
| 이름 프로세스명 로그 규칙명 | 해당 정책의 이름을 표시합니다 |
| 요약 | 지정된 정책을 간략하게 보여줍니다. |
| 서버 대수 | 해당 정책을 사용하는 서버의 수를 표시합니다. |

**모니터링 알림 정책**

서버의 재시작 여부, 에이전트의 통신 장애 지속시간, 자원 사용량에 따라 알림 발생 여부를 설정할 수 있습니다.[![1480](https://github.com/jinronara/deleteme_2/raw/master/images/1480.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1480.png)

| 이름 | 설명 |
| :--- | :--- |
| 통신 장애 알림 | 지정된 지속기간 동안 에이전트가 반응이 없을 경우 알림 발생 여부를 설정합니다. |
| CPU Memory Swap | CPU, Memory, SWAP 메모리 등의 사용률에 대한 알림을 설정합니다. |
| Disk | 디스크 사용량과 I/O 사용량을 기반으로 알림을 설정합니다. |
| Network | 네트워크 사용량과 관련한 알림을 설정합니다. 트래픽 양과 초당 패킷을 기준으로 설정할 수 있습니다. |
| 지속시간 | 해당 시간 이후 서버의 상태가 Warning, Fatal로 변경됩니다. |

* 주의 : 하나의 서버는 하나의 알림 정책만을 할당 받을 수 있습니다.

**프로세스 알림 정책**

**프로세스 알림 정책 설정**

특정 프로세스에 대한 알림 정책을 설정할 수 있습니다.[![1490](https://github.com/jinronara/deleteme_2/raw/master/images/1490.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1490.png)

1. 프로세스명: 선택한 프로세스명이 표기됩니다.
2. Enable as Project-Wide: 해당 프로젝트에 있는 모든 서버들에 해당 알람 정책을 적용합니다.
3. Count: 해당 프로세스의 개수 증감에 대하여 알림을 설정할 수 있습니다. 좌측의 경우 최저치 알림 / 우측의 경우 최대치 알림입니다.
   * 만약 프로세스가 슬라이더 좌측보다 적어지면 알림이 발생하고, 반대로 슬라이더 우측보다 많아지면 알림이 발생합니다.
4. CPU: CPU 사용량에 따라 알림을 설정할 수 있습니다.
5. Memory: 메모리 사용량에 따라 알림을 설정할 수 있습니다.
6. 알림 정책 적용: 해당 프로세스에 대한 알림을 단일 서버가 아닌 다중 서버에 대한 정책으로 설정할 수 있습니다.
7. 임계값 지속 시간: 해당 설정된 임계값의 지속시간 이후 서버 상태가 Warning 혹은 Fatal로 변경됩니다.

**로그 알림 정책**

로그 정책은 애플리케이션에서 발생하는 여러 로그들의 감시 설정을 편리하게 관리할 수 있도록 만들어졌습니다.

**로그 알림 정책 설정**

[![1500](https://github.com/jinronara/deleteme_2/raw/master/images/1500.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1500.png)

1. 해당 정책의 이름을 지정합니다.
2. 새로운 규칙을 생성합니다.
3. 지정된 규칙을 삭제합니다.
4. 삭제하거나 적용될 규칙을 선택합니다.
5. 적용될 서버를 선택합니다.

**파일 로그**

[![1510](https://github.com/jinronara/deleteme_2/raw/master/images/1510.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1510.png)

파일 로그를 감시하기 위해 파일 경로, 키워드를 입력할 수 있습니다. \* 파일 경로: 감시할 파일의 경로 \* 키워드: 해당 파일의 로그에서 해당 키워드가 발생시 알림을 발생시킵니다. \* 위험도: 알림이 발생하였을 때 위험도를 지정합니다.

**이벤트 로그**

[![1520](https://github.com/jinronara/deleteme_2/raw/master/images/1520.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1520.png)

이벤트 로그를 감시하기 위해 로그명, 수준을 선택할 수 있으며, 이벤트 소스, 이벤트 ID, 키워드를 입력할 수 있습니다. 각각의 빈칸에는 아래의 사진들에서 지정된 영역에 해당하는 값들 중에서 모니터링 하고자 하는 값을 골라 기입하시면 됩니다.[![1530](https://github.com/jinronara/deleteme_2/raw/master/images/1530.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1530.png)[![1540](https://github.com/jinronara/deleteme_2/raw/master/images/1540.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1540.png)

* 위험도: 알림이 발생했을 때 해당 알림의 위험도를 지정할 수 있습니다.
* 이벤트 로그는 Windows 환경에서만 사용 가능합니다.

**알림 내역**

해당 프로젝트에 등록된 모든 서버에서 발생한 모든 알림 내역 리스트를 볼 수 있으며, 서버명을 기준으로 검색할 수 있습니다.[![1550](https://github.com/jinronara/deleteme_2/raw/master/images/1550.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1550.png)

| 이름 | 설명 |
| :--- | :--- |
| 발생시간 | 알림 발생시간 |
| 위험도 | Fatal\(위험\) 혹은 Warning\(경고\)로 표시됩니다. |
| 서버명 | 서버 이름 |
| 설명 | 알림 정책에서 설정한 값을 바탕으로 발생한 알림 설명 |
| 스냅샷 | 발생한 알림에 대한 CPU, Memory, Disk, Network에 대한 스냅샷 정보 |
| 현재상태 | 해당 알림의 현재 상태 |
| 처리내역 | 알림에 대한 처리내역 |

7.2.4.3. 알림 상세 정보 알림 내역에서 하나의 알림을 선택 시 상세 정보 페이지로 이동합니다.[![1560](https://github.com/jinronara/deleteme_2/raw/master/images/1560.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1560.png)

1. 개요: 발생한 알림에 대한 개요를 확인할 수 있습니다.
2. 발생한 시점의 전후로 5분씩의 CPU, Memory, Disk, Network 차트를 보여줍니다. 알림에 해당하는 부분의 Severity\(위험도\)를 표시하고 있습니다.
3. 알림에 해당하는 프로세스 정보를 상위로부터 10개를 보여주고 있으며, View all 링크를 클릭시 모든 프로세스 정보를 확인할 수 있습니다.
   * 해당 화면에서도 각각의 프로세스에 대한 알림 정책을 설정할 수 있습니다.
4. 알림에 대한 처리 내역 리스트를 보여줍니다. Acknowledge Add버튼을 눌러 처리내역을 추가적으로 기입 후 저장할 수 있습니다.

#### 보고서 {#user-content-보고서-1}

**일일 보고서 \(전체 요약\)**

하루 동안 수집한 데이터를 토대로 보고서를 작성해 보여줍니다.[![1570](https://github.com/jinronara/deleteme_2/raw/master/images/1570.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1570.png)

* 보고서를 작성할 데이터 기간을 설정합니다. 시간 설정 버튼을 눌러 시작~종료 시간을 설정할 수 있습니다.
* 이메일 수신을 체크면 매일 오전 중 일일 보고서를 이메일로 전달 받을 수 있습니다.
* 인쇄 버튼을 누르면 해당 보고서를 인쇄할 수 있습니다.
* 프로젝트 이름, 서버 대수, 알림 개수를 보여줍니다.
  * Change rate는 전날 대비 증감폭입니다.
* 서버 이름, CPU/메모리 평균, 알림 개수를 요약해서 보여줍니다.
* 당일 발생한 알림의 발생 시간, 위험도, 서버명, 설명, 스냅샷을 최대 50개까지 보여줍니다.

**주간 보고서**

일주일 동안 수집한 데이터를 토대로 보고서를 작성해 보여줍니다.[![1580](https://github.com/jinronara/deleteme_2/raw/master/images/1580.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1580.png)

* 보고서를 작성할 데이터 기간을 설정합니다.
* 내보내기 버튼을 누를 경우 .CSV 형식으로 보고서를 저장합니다.
* 인쇄 버튼을 누를 경우 해당 보고서를 인쇄할 수 있습니다.
* 서버 이름, CPU Avg\(%\), Memory Avg\(%\)를 요약해서 보여줍니다.   ==== 주간 보고서 \(디스크\) 일주일간 수집한 데이터 중 디스크만 추출하여 보고서를 작성해 보여줍니다.

[![1590](https://github.com/jinronara/deleteme_2/raw/master/images/1590.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1590.png)

* 보고서를 작성할 데이터 기간을 설정합니다, 설정한 날짜의 이후 7일간의 데이터를 보여줍니다.
* 내보내기 버튼을 누를 경우 .CSV 형식으로 보고서를 저장합니다.
* 인쇄 버튼을 누를 경우 해당 보고서를 인쇄할 수 있습니다.
* 서버 이름, Disk\(%\)를 요약해서 보여줍니다.   ==== 월간 보고서 한달 동안 수집한 데이터를 토대로 보고서를 작성해 보여줍니다.

[![1600](https://github.com/jinronara/deleteme_2/raw/master/images/1600.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1600.png)

* 보고서를 작성할 데이터 기간을 설정합니다.
* 내보내기 버튼을 누를 경우 .CSV 형식으로 보고서를 저장합니다.
* 인쇄 버튼을 누를 경우 해당 보고서를 인쇄할 수 있습니다.
* 서버 이름, CPU Avg\(%\), Memory Avg\(%\)를 요약해서 보여줍니다.

**월간 보고서 \(디스크\)**

한달간 수집한 데이터 중 디스크 정보만 추출하여 월간 보고서를 작성하여 보여줍니다.[![1610](https://github.com/jinronara/deleteme_2/raw/master/images/1610.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1610.png)

* 보고서를 작성할 데이터 기간을 설정합니다. 설정한 기간 이후의 1달간 데이터를 보고서로 작성합니다.
* 내보내기 버튼을 누를 경우 .CSV 형식으로 보고서를 저장합니다.
* 인쇄 버튼을 누를 경우 해당 보고서를 인쇄할 수 있습니다.
* 서버 이름, 사용 경로, Disk\(%\)를 요약해서 보여줍니다.

**월간 보고서 \(애플리케이션 상세\)**

한달간 수집한 데이터를 토대로 애플리케이션 별 월간 보고서를 작성하여 보여줍니다.[![1620](https://github.com/jinronara/deleteme_2/raw/master/images/1620.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1620.png)

* 보고서를 작성할 데이터 기간을 설정합니다.
* 내보내기 버튼을 누를 경우 .CSV 형식으로 보고서를 저장합니다.
* 인쇄 버튼을 누를 경우 해당 보고서를 인쇄할 수 있습니다.
* CPU
  * SYS
  * USR
  * STEAL
  * NICE
  * IRQ
  * SOFT\_IRQ
* MEMORY
  * MEMORY
  * SWAP
* DISK I/O
* Network

### 데이터베이스 모니터링 \(준비 중\) {#user-content-데이터베이스-모니터링-준비-중}

### 통합 \(준비 중\) {#user-content-통합-준비-중}

#### 그룹 관리 {#user-content-그룹-관리}

**그룹 추가**

와탭 콘솔의 좌측 탭에 있는 그룹 추가 버튼을 눌러 그룹을 생성합니다.[![1630](https://github.com/jinronara/deleteme_2/raw/master/images/1630.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1630.png)

생성창에 그룹 명과 그룹에 대한 설명을 적으신 후 생성버튼을 눌러 그룹을 생성합니다.[![1640](https://github.com/jinronara/deleteme_2/raw/master/images/1640.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1640.png)

**그룹 멤버**

{text 그룹 멤버 관련 내용 필요}

**프로젝트 그룹화**

프로젝트를 생성할 때 그룹을 정할 수 있습니다.[![1650](https://github.com/jinronara/deleteme_2/raw/master/images/1650.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1650.png)

프로젝트를 생성한 이후에는 프로젝트의 우측 상단에 있는 더보기 버튼을 눌러 그룹을 이동할 수 있습니다.[![1660](https://github.com/jinronara/deleteme_2/raw/master/images/1660.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1660.png)[![1670](https://github.com/jinronara/deleteme_2/raw/master/images/1670.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1670.png)

**그룹 삭제**

**프로젝트 그룹 삭제**

프로젝트의 그룹만 삭제하고 싶다면 프로젝트 우측 상단에 존재하는 더보기 버튼을 눌러 그룹 삭제 버튼을 눌러 삭제합니다.[![1680](https://github.com/jinronara/deleteme_2/raw/master/images/1680.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1680.png)[![1690](https://github.com/jinronara/deleteme_2/raw/master/images/1690.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1690.png)

**그룹 삭제**

그룹 자체를 삭제하고 싶은 경우 그룹탭의 그룹명 우측에 존재하는 더보기 버튼을 누른 뒤 그룹 삭제 버튼을 눌러 그룹을 삭제합니다.[![1700](https://github.com/jinronara/deleteme_2/raw/master/images/1700.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1700.png)[![1710](https://github.com/jinronara/deleteme_2/raw/master/images/1710.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1710.png)

#### 그룹 사용 {#user-content-그룹-사용}

[![1720](https://github.com/jinronara/deleteme_2/raw/master/images/1720.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1720.png)

와탭 모니터링 서비스는 기본값으로 프로젝트 단위로 구성되어 작동합니다. 프로젝트에 속한 SuperAdmin은 프로젝트 관리 뿐만 아니라, 청구의 대상이 됩니다.

하지만, 동일한 조직 내에 다양한 목적의 프로젝트를 수행할 경우 프로젝트 단위만으로 관리하는 것이 어려울 수 있습니다. 그렇기 때문에 와탭에서는 별도의 효율적으로 조직간 관리를 할 수 있도록 그룹 기능을 제공하고 있습니다.

그룹은 대시보드 화면의 좌측에 속한 버튼으로 나타납니다. 한 개의 그룹에는 한 명의 Owner가 존재하며, 한 개의 그룹은 여러개의 프로젝트를 가질 수 있습니다.. 특정 그룹 버튼의 우측에 있는 버튼을 누르면 해당 그룹에 따른 옵션을 볼 수 있습니다. 그룹에 속한 유저별로 별도의 권한을 부여받습니다.

|  | 그룹 소유 | 주 청구 계정 | 그룹 생성, 편집, 삭제 | 그룹 유저 계정 권한 변경 | 그룹 유저 삭제 | 그룹 프로젝트 열람 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Owner | O | O | O | O | O | O |
| Admin |  |  |  | O | O | O |
| User |  |  |  |  |  | O |

**프로젝트 그룹 등록**

새롭게 만드는 프로젝트와 기존에 생성되어 있는 프로젝트 모두 그룹에 등록할 수 있습니다. 단, 프로젝트는 그룹에 등록할 때 다른 그룹에 등록되어 있을 수 없습니다.

* 1개의 프로젝트는 1개의 그룹에만 속할 수 있습니다.

새롭게 생성한 프로젝트를 그룹에 등록하고자 하는 경우, 해당 그룹에 들어간 뒤, 프로젝트를 생성해주면 됩니다.[![1730](https://github.com/jinronara/deleteme_2/raw/master/images/1730.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1730.png)

기존에 있는 프로젝트를 그룹에 등록하고자 하는 경우, 대시보드를 그룹뷰의 형태로 변경한 후, 해당 프로젝트의 우측에 있는 버튼을 클릭합니다.[![1740](https://github.com/jinronara/deleteme_2/raw/master/images/1740.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1740.png)

해당 화면에서 희망하는 그룹으로 선택하면 이동됩니다.

**프로젝트 그룹 이동**

그룹 이동은 앞서 설명된 그룹 등록과 같습니다. 하지만, 1개의 프로젝트는 1개의 그룹에만 속할 수 있기 때문에 그룹을 이전하고자 하는 경우 &lt;1.3. 프로젝트 그룹 삭제&gt; 에서 설명한 방법대로 기존의 그룹으로부터 삭제한 후, 진행해야합니다.

**프로젝트 그룹 삭제**

그룹에 속해있는 프로젝트를 그룹으로부터 삭제하고자 하는 경우, 그룹 삭제 기능을 이용하면 됩니다. 그룹으로부터 삭제된 프로젝트는 All에서만 보실 수 있으며, 다른 그룹으로 재배치가 가능합니다.[![1750](https://github.com/jinronara/deleteme_2/raw/master/images/1750.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1750.png)

**그룹 삭제**

[![1760](https://github.com/jinronara/deleteme_2/raw/master/images/1760.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1760.png)

그룹 Owner 권한을 가진 유저의 경우, 해당 그룹을 삭제할 수 있습니다. 해당 그룹 버튼 우측에 있는 버튼을 누른 뒤 그룹 삭제를 선택하면 됩니다. 그룹 삭제는 해당 그룹과 더불어 속해있던 사용자 목록 정보도 삭제됩니다. 다만 삭제 된 뒤에도 프로젝트는 그룹 정보만 삭제되며 최종 관리자 권한이 SuperAdmin으로 귀속됩니다.

* 그룹을 삭제한 뒤에는 복구하실 수 없습니다. 주의해주시기 바랍니다.

**청구 계정 통일**

[![1770](https://github.com/jinronara/deleteme_2/raw/master/images/1770.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1770.png)

* 그룹을 사용하지 않고 SuperAdmin이 청구의 단위가 될 경우

와탭 모니터링 서비스의 청구 단위는 SuperAdmin 계정 단위로 발생합니다. 프로젝트 4개가 각각 다른 SuperAdmin 계정으로 되어 있다면 청구는 총 4개의 아이디를 대상으로 됩니다. 사내에서 별도로 프로젝트를 관리하며 청구 계정은 동일하게 유지하고자 하는 경우, &lt;그룹&gt; 기능을 이용하여 하나의 아이디로 관리해주시기 바랍니다.[![1780](https://github.com/jinronara/deleteme_2/raw/master/images/1780.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1780.png)

* 그룹을 사용하여 단일 Owner가 청구의 단위가 될 경우

기존에는 SuperAdmin이 청구의 대상이 되었었지만, 그룹에 배치하여 모니터링을 진행할 경우, 청구의 대상은 가장 높은 단계에 있는 Owner가 됩니다. 이 경우 각각의 SuperAdmin의 청구 정보를 등록하지 않아도 Owner로 등록된 한 사람이 모든 청구업무를 맡을 수 있습니다.

#### 그룹뷰 {#user-content-그룹뷰}

**개요**

복수의 프로젝트를 그룹핑하여 관리하고 통합 모니터링 하기 위한 기능을 제공합니다.

**그룹뷰 설정**

와탭 콘솔에서 그룹뷰 버튼을 클릭하고 수정 버튼을 클릭합니다.[![1790](https://github.com/jinronara/deleteme_2/raw/master/images/1790.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1790.png)

좌측에 표시되는 차트 중 조합하고자 하는 차트를 클릭하면 우측에 차트가 표시될 영역에 차트가 추가됩니다. 우측 상단의 더보기 버튼을 클릭하여 차트에 표시할 대상 프로젝트를 선택합니다.[![1800](https://github.com/jinronara/deleteme_2/raw/master/images/1800.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1800.png)

* 추가된 차트의 우측 하단을 드래그하여 차트의 사이즈를 조정하고, 차트를 클릭한 채로 이동하여 차트를 표시할 위치를 지정합니다.

설정이 완료되었으면 Save 버튼을 클릭하여 저장하고, Complete 버튼을 클릭하여 종료합니다. 잠시 기다리면 모니터링 정보가 표시됩니다.[![1810](https://github.com/jinronara/deleteme_2/raw/master/images/1810.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1810.png)

**그룹뷰 활용 예시**

[![1820](https://github.com/jinronara/deleteme_2/raw/master/images/1820.png)](https://github.com/jinronara/deleteme_2/blob/master/images/1820.png)

#### 멀티 프로젝트 연관뷰 \(준비 중\) {#user-content-멀티-프로젝트-연관뷰-준비-중}

### 빌링 \(준비 중\) {#user-content-빌링-준비-중}

#### 결제 절차 {#user-content-결제-절차}

**SMS**

**애플리케이션/인프라**

#### 지불 수단 등록 {#user-content-지불-수단-등록}

**카드 등록**

**계좌 이체 등록**

#### SMS 상품 구매 {#user-content-sms-상품-구매}

#### 애플리케이션/인프라 프로젝트 유상 전환 {#user-content-애플리케이션-인프라-프로젝트-유상-전환}

#### 지불 내역 확인 {#user-content-지불-내역-확인}

