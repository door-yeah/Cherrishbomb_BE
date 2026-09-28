# 🍒 Cherrishbomb

> 엣지 디바이스가 감지한 **낙상 이벤트를 실시간으로 받아 보호 기관·보호자에게 보여주는** 모니터링 서비스

## 📌 소개

고령자·환자의 낙상은 발견이 늦어질수록 위험이 커집니다.
Cherrishbomb은 현장에 설치된 엣지 디바이스가 낙상을 감지하면, 그 데이터를 서버로 전달받아
기관 관리자와 보호자가 **언제, 어디서, 누가** 넘어졌는지 바로 확인할 수 있도록 합니다.

## 🏗 시스템 구조

```
┌──────────────┐   낙상 이벤트    ┌──────────────┐    조회 / 알림     ┌──────────────┐
│ Edge Device  │ ───────────────▶ │  Cherry_BE   │ ─────────────────▶ │  Cherry_FE   │
│ (낙상 감지)  │                  │ (Spring Boot)│                    │ (기관·보호자)│
└──────────────┘                  └──────┬───────┘                    └──────────────┘
                                         │
                                    ┌────▼────┐
                                    │  MySQL  │
                                    └─────────┘
```

| 구성 요소 | 역할 |
|---|---|
| **Edge Device** | 현장에서 낙상을 감지하고 이벤트를 서버로 전송 |
| **Cherry_BE** | 이벤트 수신·저장, 기관/사용자 관리, 조회 API 제공 |
| **Cherry_FE** | 기관 관리자·보호자가 낙상 기록과 현황을 확인하는 화면 |

## ✨ 주요 기능

- **낙상 이벤트 수신** — 엣지 디바이스가 보낸 감지 데이터를 받아 저장
- **낙상 기록 조회** — 발생 시각, 위치, 대상자별 이력 확인
- **기관 회원가입 / 로그인** — 요양원·병원 등 보호 기관 단위로 계정 관리
- **소셜 로그인** — Google, Kakao OAuth + JWT 인증

## 🛠 기술 스택

| 분류 | 기술 |
|---|---|
| Backend | Java 21, Spring Boot 4, Lombok |
| Database | MySQL |
| Auth | OAuth 2.0 (Google, Kakao), JWT |
| DevOps | Docker, GitHub Actions |
| Collaboration | CodeRabbit (AI 코드 리뷰), GitHub Issues / PR 템플릿 |

## 📁 프로젝트 구조

```
Cherrishbomb_BE
├── Cherry_BE/                     # Spring Boot 백엔드
│   └── src/main/java/com/example/Cherry_BE
│       └── domain/
│           └── organization/      # 기관(회원) 도메인
│               ├── controller/
│               ├── service/
│               ├── repository/
│               ├── entity/
│               └── dto/
├── Cherry_FE/                     # 프론트엔드
├── .github/                       # CI, 이슈·PR 템플릿
└── Dockerfile
```

## 🚀 실행 방법

```bash
cd Cherry_BE
./gradlew bootRun
```

실행 전 아래 환경변수가 필요합니다.

| 변수 | 설명 |
|---|---|
| `MYSQL_USERNAME` / `MYSQL_PASSWORD` | DB 접속 정보 |
| `GOOGLE_CLIENT_ID` / `GOOGLE_CLIENT_SECRET` | Google OAuth |
| `KAKAO_CLIENT_ID` / `KAKAO_CLIENT_SECRET` | Kakao OAuth |
| `JWT_SECRET` | JWT 서명 키 |
| `JWT_ACCESS_TOKEN_MINUTES` / `JWT_REFRESH_TOKEN_DAYS` | 토큰 만료 시간 |
| `APP_AUTH_REDIRECT_URI` | 로그인 후 리다이렉트 주소 |

## 👥 팀

| 이름 | 역할 |
|---|---|
| [@door-yeah](https://github.com/door-yeah) | Backend — 낙상 데이터 수신·조회 API, 기관 도메인 |
| [@ChanWooong](https://github.com/ChanWooong) | CI/CD, 협업 환경 구성 |
