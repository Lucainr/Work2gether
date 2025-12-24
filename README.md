<div align="center">

<img src="https://img.shields.io/badge/Work2gether-Groupware_Platform-0f172a?style=for-the-badge" alt="Work2gether" />

# Work2gether

### Spring MVC 기반 통합 그룹웨어 (계약사 멀티 테넌트)

<br />

<p align="center">
  <img src="https://img.shields.io/badge/Java-11+-b07219?style=flat-square&logo=openjdk" />
  <img src="https://img.shields.io/badge/Spring_Framework-5.3-6db33f?style=flat-square&logo=spring" />
  <img src="https://img.shields.io/badge/Spring_Security-5.7-6db33f?style=flat-square&logo=springsecurity" />
  <img src="https://img.shields.io/badge/MyBatis-3.5-d71f00?style=flat-square" />
  <img src="https://img.shields.io/badge/Oracle_JDBC-ojdbc8-f80000?style=flat-square&logo=oracle" />
  <img src="https://img.shields.io/badge/HikariCP-4.0-0ea5e9?style=flat-square" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Tiles_JSP-View-2563eb?style=flat-square" />
  <img src="https://img.shields.io/badge/WebSocket-/echo-0f766e?style=flat-square" />
  <img src="https://img.shields.io/badge/Gmail_API-OAuth-ef4444?style=flat-square&logo=gmail" />
  <img src="https://img.shields.io/badge/AWS-S3-ff9900?style=flat-square&logo=amazonaws" />
  <img src="https://img.shields.io/badge/CoolSMS-Alarm-6366f1?style=flat-square" />
  <img src="https://img.shields.io/badge/PDFBox%20%7C%20POI-Docs-9333ea?style=flat-square" />
</p>

<br />

**근태·일정 · 전자결재 · 메신저 · 메일 · 계약/통계 · 파일스토리지**를 하나로 제공하는 B2B 그룹웨어  

<br />

[🚀 시작하기](#-getting-started) · [⚙️ 설정](#-configuration) · [🧭 주요 흐름](#-주요-흐름--url) · [🏗️ 아키텍처](#-architecture) · [🛠️ 기술 스택](#-tech-stack)

</div>

<br />

---

## 📌 Overview

Work2gether는 계약사별(회사 ID) 경로로 격리된 멀티 테넌트 환경에서 전자결재, 메일, 메신저, 근태/휴가, 일정/회의실, 프로젝트/To-Do, 지출/계약/통계를 제공하는 Spring MVC 기반 그룹웨어 서비스입니다. WAR로 패키징해 Tomcat 등 서블릿 컨테이너에 배포하며, JSP+Tiles와 WebSocket, MyBatis, Spring Security를 핵심으로 사용합니다.

<br />

## ✨ Key Features

<table>
<tr>
<td width="50%">

### 🧭 업무/조직
- 회사별 `/ {companyId}/main` 대시보드
- 부서/직급/조직도/사원 관리, 발령 이력 관리
- 프로젝트 & 개인 To-Do, 공지/문의 게시판, 설문조사
- 회의실·자원·시간 예약, 일정/색상/유형 관리

</td>
<td width="50%">

### 🧾 전자결재/문서
- 결재 문서/양식/라인/참조/승인 흐름
- 첨부파일 업로드(로컬/S3), PDF/Excel 출력
- 결재 진행/완료/참조 문서 뷰어

</td>
</tr>
<tr>
<td width="50%">

### 🔐 보안/계정
- Spring Security 로그인(`/a001/login`)
- 동적 자원 권한 매핑, Anonymous/Authenticated 구분
- Locale 쿠키, 메시지 번들 다국어 지원
- HTTPS 강제(`CONFIDENTIAL`) 설정

</td>
<td width="50%">

### 💬 커뮤니케이션
- WebSocket 메신저 `/echo?userId=` (1:1 알림)
- Gmail API 연동(수신/발신/임시저장/중요/휴지통)
- 내부 쪽지함(발신·수신·매핑·휴지통)

</td>
</tr>
<tr>
<td width="50%">

### 📊 계약/정산/통계
- 계약 생성/초기 설정 온보딩(`/setupPage/**`)
- 프로바이더 포털 `/prov/**` 계약 분석·필터·결제 이력
- 지출/경비/결제(PG) 내역, 통계 대시보드

</td>
<td width="50%">

### ☁️ 스토리지
- 로컬 저장소 경로 관리(`DirectoryInfo.properties`)
- AWS S3 업로드(키 주입 방식)
- 첨부파일/클라우드 저장소 모듈

</td>
</tr>
</table>

<br />

---

## 🖼 Preview

- 로그인/보안: `/a001/login`, 로그인 후 `/{companyId}/main`
- 전자결재: `/approval/*`
- 메일: `/mail/*` (Gmail API 연동), WebSocket 알림 `/echo`
- 프로바이더 포털: `/prov/main`, `/prov/*`
- 온보딩 플로우: `/setupPage/firstSet` → `/setupPage/previewSetupPage` → `/setupPage/firstSave` → `/setupPage/firstSetsuccess`

<br />

---

## 🛠️ Tech Stack

### Application
| Category | Technologies |
|----------|--------------|
| **Language** | Java 11+ |
| **Framework** | Spring Framework 5.3 (MVC, Security 5.7, WebSocket) |
| **Persistence** | MyBatis 3.5, HikariCP, Oracle JDBC (ojdbc8) |
| **View** | JSP, JSTL, Tiles, Sneat UI 리소스 |
| **Validation** | JSR-303 (Hibernate Validator) |
| **Messaging** | WebSocket `/echo` (SockJS 폴백 설정) |
| **Docs/Files** | Apache POI, PDFBox, Thumbnailator |

### Integrations
| Category | Technologies |
|----------|--------------|
| **Auth/OAuth** | Google OAuth + Gmail API |
| **Storage** | AWS S3 SDK |
| **SMS** | CoolSMS SDK |
| **JSON** | Jackson 2.18, Gson 2.11 |

### Build & Test
| Category | Technologies |
|----------|--------------|
| **Build** | Maven 3.9, WAR packaging (`work2gether.war`) |
| **Server** | Servlet 3.1+, Tomcat 9+ |
| **Testing** | JUnit 5, Spring Test (SpringJUnitWebConfig) |
| **Logging** | Log4j2, SLF4J, log4jdbc |

<br />

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────┐
│                 Clients                     │
│  Web (JSP/Tiles, JS/CSS from /resources)    │
└─────────────────────────────────────────────┘
                      │
           ┌──────────┴──────────┐
           ▼                     ▼
┌──────────────────────┐   ┌───────────────────┐
│   Spring MVC App     │   │   WebSocket `/echo`│
│ DispatcherServlet    │   │ Text handler (user │
│ Controllers/Services │   │ -> session map)    │
└──────────────────────┘   └───────────────────┘
           │
           ▼
┌─────────────────────────────────────────────┐
│ MyBatis + HikariCP + Oracle (ojdbc8)        │
│ Mapper XML: attendance/approval/contract/...│
└─────────────────────────────────────────────┘
           │
┌──────────┼──────────────────────────────────┐
│  External Services                          │
│  - Gmail API (OAuth)                        │
│  - AWS S3 (uploads)                         │
│  - CoolSMS (notifications)                  │
└─────────────────────────────────────────────┘
```

<br />

---

## 📂 Project Structure

```
Team02Final/
├── pom.xml                     # Maven, WAR(build: work2gether)
├── src/
│   ├── main/java/kr/or/ddit/
│   │   ├── commons/            # Index, util, advice, websocket(EchoHandler)
│   │   ├── security/           # WebSecurity config, handlers, authz manager
│   │   ├── account|employee|department|position|organitree
│   │   ├── attendance|vacation|schedule|room|roomTime|timeReservation
│   │   ├── project|todolist|message|gmail
│   │   ├── approval|expense|payment|statistics
│   │   ├── contract|provider|teamHistory
│   │   └── cloud|aws|atch      # Storage, S3, attachments
│   ├── main/resources/
│   │   ├── kr/or/ddit/spring/context-*.xml   # common, datasource, mapper, tx, msg, aop
│   │   ├── kr/or/ddit/mybatis/mappers/**     # mapper XML
│   │   └── log4j2.xml, log4jdbc.log4j2.properties
│   └── main/webapp/
│       ├── WEB-INF/web.xml, springmvc/dispatcher-servlet.xml, websocket-context.xml
│       ├── WEB-INF/tiles/tiles.xml
│       ├── WEB-INF/views/**   # 기능별 JSP (approval, gmail, provider, ...)
│       └── resources/**       # JS/CSS/img (Sneat 테마 포함)
└── target/work2gether.war
```

<br />

---

## 🚀 Getting Started

### Prerequisites

```
✅ JDK 11+
✅ Maven 3.9+
✅ Oracle DB 19c/XE (or 호환)
✅ Tomcat 9+ (Servlet 3.1+) with HTTPS 설정
```

### Quick Start (로컬)

```bash
# 1) 의존성 설치 및 빌드
mvn clean package

# 2) 산출물
ls target/work2gether.war

# 3) Tomcat에 배포 후 접속
#    로그인:       http(s)://localhost:8080/work2gether/a001/login
#    대시보드:     http(s)://localhost:8080/work2gether/{companyId}/main
#    프로바이더:   http(s)://localhost:8080/work2gether/prov/main
```

<br />

---

## ⚙️ Configuration

### 1) Database (필수)
`src/main/resources/kr/or/ddit/db/DBInfo.properties` 생성
```properties
driverClassName=oracle.jdbc.driver.OracleDriver
url=jdbc:oracle:thin:@localhost:1521/xe
user=your_username
password=your_password
testQuery=SELECT 1 FROM DUAL
minimulIdle=2
maximulSize=10
maxWait=30000
```

### 2) 파일 저장소
`src/main/resources/kr/or/ddit/DirectoryInfo.properties`
```properties
saveDir=file:/path/to/saveDir/
```
`dispatcher-servlet.xml`에서 `/images/**`가 물리 경로(기본 `file:///D:/multipartDir/saveDir/`)와 매핑되어 있으므로 동일하게 설정

### 3) HTTPS
`web.xml`의 `user-data-constraint`가 `CONFIDENTIAL`로 설정되어 있다. 로컬 HTTP가 필요하면 임시로 해당 제약을 조정하고, 운영 배포 시 HTTPS 커넥터를 유지

### 4) 외부 연동 키
- **AWS S3**: 액세스/시크릿 키를 환경/DB에 저장 후 `aws.connection.GetAWSUser`에서 사용
- **Gmail API**: OAuth Client/Refresh Token을 발급해 DB/환경에 저장, `gmail` 서비스가 REST 호출 시 사용
- **CoolSMS**: API 키/시크릿을 환경에 저장 후 알림 전송에 사용

### 5) 로깅
- `log4j2.xml`, `log4jdbc.log4j2.properties`로 애플리케이션/SQL 로깅 분리. SQL 로그가 필요하면 log4jdbc 설정을 활성화

### 6) 업로드 한도/멀티파트
`web.xml`에서 `MultipartFilter`가 활성화되어 있으며, 파일 한도는 CommonsMultipartResolver 주석 설정을 참고해 필요 시 조정

<br />

---

## 🧭 주요 흐름 / URL

- 로그인: `/a001/login` → 인증 성공 시 `/{companyId}/main`
- 온보딩(계약사 초기 설정): `/setupPage/firstSet` → `/setupPage/previewSetupPage` → `/setupPage/firstSave` → `/setupPage/firstSetsuccess`
- 프로바이더 포털: `/prov/main`, `/prov/*` (계약 분석/통계/결제 이력)
- 전자결재: `/approval/*` (문서·양식·라인·참조·결재 처리)
- 메일: `/mail/*` + Gmail API, WebSocket 알림 `/echo?userId={id}`
- 정적 리소스: `/resources/**`, 업로드 파일: `/images/**`(물리 경로 매핑)

<br />

<div align="center">

<br />

[⬆️ Back to Top](#work2gether)

</div>
