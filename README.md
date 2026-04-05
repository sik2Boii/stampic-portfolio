# 📱 스탬픽(Stampic) Backend — 포트폴리오

> 실제 운영 중인 모바일 애플리케이션의 백엔드 개발, 배포, 운영 경험을 담은 포트폴리오입니다.

> 원본 레포지토리는 실운영 중인 서비스로 보안상 Private으로 관리되고 있습니다.

---

## 📲 다운로드 링크

[![App Store](https://img.shields.io/badge/App_Store-0D96F6?style=for-the-badge&logo=app-store&logoColor=white)](https://apps.apple.com/kr/app/스탬픽/id6756785730)
[![Google Play](https://img.shields.io/badge/Google_Play-414141?style=for-the-badge&logo=google-play&logoColor=white)](https://play.google.com/store/apps/details?id=com.project.stampy&hl=ko)

---

## 📸 서비스 화면 (Preview)

**1. 일상의 수집 (내 기록 조회)**
> ![Image](https://github.com/user-attachments/assets/0ce33973-734c-490d-9618-6938c9b6c5c9)

**2. 순간의 완성 (스탬프 카메라 촬영 및 적용)**
> ![Image](https://github.com/user-attachments/assets/ba5be1d2-4ef7-42ec-93f7-0b6c8ced3e5f)

**3. 기록의 연결 (커뮤니티 피드)**
> ![Image](https://github.com/user-attachments/assets/e7f2c5bc-347b-451d-8def-9017b8bc40cb)

---

## 📌 프로젝트 개요

**스탬픽(Stampic)** 은 일상 중 순간의 사진을 타임스탬프로 기록하고 공유하는 모바일 커뮤니티 애플리케이션입니다.

| 항목 | 내용 |
|------|------|
| **MVP 개발** | 2025.11 ~ 2026.01 |
| **고도화** | 2026.01 ~ 현재 (진행 중) |
| **역할** | 백엔드 개발, 배포, 운영 (백엔드 2인 중 1인) |
| **상태** | App Store, Google Play 실배포 운영 중 |
| **누적 가입자** | 130명+ |

---

## 👥 팀 구성 및 협업

**총 7명 팀 프로젝트**

| 역할 | 인원 |
|------|------|
| PM | 1명 |
| 디자이너 | 2명 |
| iOS 개발자 | 1명 |
| Android 개발자 | 1명 |
| 백엔드 개발자 | 2명 |

**담당 업무**
- 시스템 아키텍처 설계: 네이버 클라우드 환경 기반 전체 시스템 아키텍처 구성 및 Presigned URL 업로드 로직 설계
- 커뮤니티 도메인 개발: 사진 공유, 좋아요 등 커뮤니티 핵심 비즈니스 로직 및 REST API 구현
- DB 성능 최적화: 커버링 인덱스 적용을 통한 대용량 커뮤니티 피드 조회 쿼리 튜닝
- 인프라 및 DevOps: GitHub Actions, Docker, Nginx를 활용한 CI/CD 자동화 파이프라인 및 블루-그린 무중단 배포 환경 구축
- 백오피스(Admin) 구현: App Store 커뮤니티 심사 가이드라인 대응을 위해 접수된 사용자 신고 내역을 검증하고 악성 콘텐츠를 관리하는 Thymeleaf 기반 관리자 웹 페이지 개발
    <details>
    <summary>📎 관리자 페이지 스크린샷 (클릭하여 펼치기)</summary>
    
    > <img width="1320" height="602" alt="Image" src="https://github.com/user-attachments/assets/64a06ab6-5a06-4179-a138-fdf4e076c6dc" />
    
    </details>

**협업 방식**
- 격주 월요일 정기 회의 기반 2주 단위 스프린트로 MVP 출시 후 지속 고도화 중
- iOS, Android 개발자와의 REST API 설계 및 조율
- Swagger 기반 API 문서화로 iOS, Android 개발자와의 명세 공유
- 디자이너와의 피드백 루프를 통한 UI/UX 기반 API 응답 설계
- 백엔드 팀원과의 코드 리뷰 및 시스템 아키텍처 설계
- GitHub PR 기반 개발 프로세스 (커밋 컨벤션, 브랜치 전략)

---

## 🛠 기술 스택

| 분류 | 기술 |
|------|------|
| **Backend** | Spring Boot 3.5.6, Java 17 |
| **API** | JWT, OAuth2, Swagger |
| **ORM** | JPA, QueryDSL |
| **Database** | MySQL |
| **Admin** | Thymeleaf |
| **Storage** | 네이버 클라우드 Object Storage |
| **Analytics** | Amplitude |
| **Monitoring** | Prometheus, Grafana |
| **DevOps** | Docker, Nginx, Certbot, GitHub Actions |
| **Cloud** | 네이버 클라우드 플랫폼 |

---

## 🏗 시스템 아키텍처

> <img width="917" height="498" alt="Image" src="https://github.com/user-attachments/assets/4e9b25a6-5b14-4752-92ad-23c2958483af" />

**핵심 설계 포인트**
- 이미지 업로드 시 서버를 거치지 않고 클라이언트 -> Object Storage 직접 업로드 (Presigned URL)
- 업로드 완료 후 서버에 메타데이터만 저장 -> 서버 부하 최소화
- 제한된 서버 리소스 환경 내에서 최적의 가용성을 확보하기 위해 단일 인스턴스 내 Nginx 포트 스위칭 기반의 블루-그린 무중단 배포 파이프라인 구축

---

## ⚡ 트러블슈팅

### 🔧 개발 중 발생

---

#### 1. 커버링 인덱스 적용 — 쿼리 성능 160배 개선

**문제 상황**

더미 데이터(게시글 100,100건 / 좋아요 2,409,198건) 기반 부하 테스트 결과  
커뮤니티 피드 조회 API 평균 응답 시간이 **약 4,000ms(4초)** 로 확인됨.

게시글 정렬(`published_at DESC, image_id DESC`) 및 게시글별 좋아요 수 집계 서브쿼리로 인해  
대량의 데이터 스캔이 발생하며 전체 피드 조회 성능에 병목이 발생하는 것으로 판단됨.

**실행계획 분석 (EXPLAIN)**

| | type | key | rows | Extra |
|---|---|---|---|---|
| **적용 전** | ALL | NULL | 2,402,103 | Using where |
| **적용 후** | ref | idx_image_like_image_user | 27 | Using index |

- 적용 전: 좋아요 테이블 전체 풀 스캔 (인덱스 미사용)
- 적용 후: 커버링 인덱스로 27건만 참조, 테이블 접근 없이 쿼리 완결

<details>
<summary>📎 실행계획 캡쳐본 보기 (클릭하여 펼치기)</summary>

**적용 전**
> <img width="1532" height="228" alt="Image" src="https://github.com/user-attachments/assets/c6542d15-1f7c-427c-81e0-459150467521" />

**적용 후**
> <img width="1466" height="174" alt="Image" src="https://github.com/user-attachments/assets/9cea2472-fe02-49da-83de-90fb5208523a" />

</details>

**해결 방안 검토**

두 가지 방법을 고려함.

| 방법 | 장점 | 단점 |
|------|------|------|
| **반정규화** (좋아요 수 컬럼 별도 관리) | 조회 시 집계 불필요, 매우 빠름 | 데이터 정합성 관리 복잡, 쓰기 부하 증가 |
| **커버링 인덱스** | 구조 변경 없이 성능 개선 가능 | 데이터가 매우 많아질 경우 한계 존재 |

- 현재 서비스 규모에서는 대규모 트래픽이 발생할 가능성이 낮고 반정규화로 인한 데이터 정합성 관리 복잡도가 더 큰 리스크라고 판단하여 **커버링 인덱스** 적용.

**해결**
- WHERE, SELECT, ORDER BY 컬럼을 모두 포함하는 **커버링 인덱스** 설계
- 테이블 접근 없이 인덱스만으로 쿼리 완결되도록 구조 개선
- QueryDSL을 활용한 최적화된 쿼리 작성

<details>
<summary>📎 응답 시간 측정 결과: 4,000ms -> 25ms (클릭하여 펼치기)</summary>

**적용 전 — 10회 요청 평균 약 4,000ms**
> ![Image](https://github.com/user-attachments/assets/caf82835-c4eb-4edf-9da6-afaf1eebd0e0)

**적용 후 — 10회 요청 평균 약 25ms**
> ![Image](https://github.com/user-attachments/assets/670040ec-510e-4c8c-8e1b-30df79146a18)

</details>

**결과**
```
⚡ 4,000ms -> 25ms (160배 개선)
✅ 좋아요 테이블 스캔 rows: 2,402,103 -> 27
✅ 데이터베이스 부하 감소
✅ 사용자 피드 응답 속도 대폭 향상
```

---

#### 2. Presigned URL 기반 이미지 업로드 — 서버 부하 최소화

**문제 상황**
- 이미지 중심 서비스 특성상 다수의 이미지 파일 업로드가 빈번하게 발생
- 서버 직접 업로드 방식의 잠재적 한계
  - 서버 메모리, 네트워크 부하 증가

**해결**
```
서버                    클라이언트                      업로드 완료 후
Presigned URL 발급  ->  Object Storage 직접 업로드  ->  서버에 메타데이터 저장
```
- 유효시간 1분으로 설정 — 실제 업로드 완료까지 수초 내외로 충분하며
  유효시간을 최소화하여 URL 유출 시 무단 업로드 피해를 방지

**결과**
```
✅ 서버 부하 최소화
✅ 이미지 업로드 안정성 확보
✅ 네트워크 효율 및 응답 속도 개선
✅ Presigned URL 유효시간 최소화로 보안 강화
```

---

### 🚨 운영 중 발생

---

#### 3. SSL 인증서 갱신 후 Nginx 미반영 — 전체 API 서버 다운 (약 7시간)

**문제 상황**
- SSL 인증서 자동 갱신 로직은 존재했으나 Nginx가 기존 인증서를 그대로 참조하여 새 인증서가 반영되지 않음
- 결과적으로 전체 API 서버 다운 발생 (다운타임 약 7시간)
- 인프라 담당자가 본인 1인이었던 관계로 업무 중 오류를 인지한 후 퇴근 즉시 조치

**해결**
1. Nginx 리로드로 즉시 서버 복구
2. 인증서 갱신 시 Nginx 자동 리로드되도록 스크립트 수정
3. 인증서 만료 전 AWS Lambda + SNS 연동으로 문자 알림 발송 구성
   - 인증서 유효기간 90일 / 연간 약 4회 발생 이벤트 -> 서버리스(Lambda)로 처리

**결과**
```
✅ 동일 장애 재발 방지
✅ 인증서 만료 전 사전 알림으로 선제 대응 체계 구축
✅ 저빈도 이벤트를 서버리스로 처리하여 리소스 효율화
```

**회고**  
- 단순한 설정 누락이 전체 시스템의 치명적인 장애로 직결될 수 있음을 경험함.
- 이를 통해 수동적인 운영을 배제하고 휴먼 에러를 방지할 수 있는 자동화와 선제적인 알림 체계가 필수적임을 깊이 체감함.

---

## 📂 주요 기능

| 기능 | 설명 |
|------|------|
| 회원 관리 | Google, Kakao, Apple OAuth2 소셜 로그인, JWT 인증 |
| 커뮤니티 피드 | 사진 공유, 조회, 좋아요 |
| 이미지 업로드 | Presigned URL 기반 Object Storage 직접 업로드 |
| API 문서화 | Swagger |
| 이벤트 분석 | Amplitude 연동 |
| 모니터링 | Prometheus + Grafana 실시간 서버 모니터링 |
| 관리자 페이지 | Thymeleaf 기반 Admin UI |
| SSL 자동화 | Certbot + Docker 기반 인증서 자동 갱신 |
| CI/CD | GitHub Actions 기반 자동 배포 |

---

## 🚀 배포 구조

```
[GitHub] main/develop 브랜치 Merge
   ↓
[GitHub Actions] 커밋 이력 기반 자동 태그(버전) 추출 및 릴리즈 노트 생성
   ↓
[GitHub Actions] Docker Image 빌드 및 Docker Hub 푸시
   ↓
[Naver Cloud] 서버에서 최신 Docker 이미지 Pull
   ↓
[Deploy] Nginx 포트 스위칭 기반 블루-그린(Blue-Green) 무중단 배포
```

---

## 📊 ERD

> <img width="1274" height="1340" alt="Image" src="https://github.com/user-attachments/assets/c2884206-39ea-482c-9beb-a38f768d370d" />

---

## 📈 운영 현황

```
누적 가입자  : 130명+
배포 플랫폼  : App Store, Google Play
운영기간     : 2026.01 ~ 현재 (3개월+)
현재        : 고도화 진행 중
```

---

## 💡 이 프로젝트를 통해 얻은 것

- **최신 기술 스택 실전 경험** — 현업(Java 8)과 다른 Spring Boot 3.x, Java 17 환경을 실무 수준으로 경험
- **팀 협업 경험** — PM, 디자이너, iOS, Android, 백엔드 7인 팀에서 크로스 플랫폼 API 설계 및 코드 리뷰 경험
- **전 사이클 경험** — 설계, 개발, 배포, 운영, 고도화까지 전체 개발 생명주기 참여
- **트레이드오프 기반 설계 판단** — 반정규화 vs 커버링 인덱스 비교 분석 후 서비스 규모에 맞는 방법 선택
- **클라우드 아키텍처** — 네이버 클라우드 Object Storage, Presigned URL 기반 업로드 설계 경험
- **무중단 배포** — 단일 인스턴스 환경에서 Nginx 포트 스위칭 기반 블루그린 배포 구현
- **모니터링 구축** — Prometheus + Grafana 기반 실시간 서버 상태 모니터링 경험
- **장애 대응 경험** — 운영 중 SSL 인증서 장애 직접 대응 및 재발 방지 체계 구축
