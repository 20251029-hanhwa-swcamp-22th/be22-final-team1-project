<p align="center">
  <img src="https://img.shields.io/badge/Java-21-007396?style=for-the-badge&logo=openjdk&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring%20Boot-3.5-6DB33F?style=for-the-badge&logo=springboot&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring%20Cloud-2025.0-6DB33F?style=for-the-badge&logo=spring&logoColor=white"/>
  <img src="https://img.shields.io/badge/Vue-3-4FC08D?style=for-the-badge&logo=vuedotjs&logoColor=white"/>
  <img src="https://img.shields.io/badge/MariaDB-10.11-003545?style=for-the-badge&logo=mariadb&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kafka-Event%20Driven-231F20?style=for-the-badge&logo=apachekafka&logoColor=white"/>
  <img src="https://img.shields.io/badge/Redis-Realtime-DC382D?style=for-the-badge&logo=redis&logoColor=white"/>
  <img src="https://img.shields.io/badge/ArgoCD-GitOps-EF7B4D?style=for-the-badge&logo=argo&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kubernetes-Orchestration-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white"/>
  <img src="https://img.shields.io/badge/AWS-Cloud-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white"/>
</p>

<h1 align="center">CONK</h1>
<h3 align="center">글로벌 풀필먼트 운영 플랫폼</h3>

<p align="center">
현지 창고를 운영하는 3PL과 셀러가 입고부터 재고, 주문, 출고, 배송, 정산까지<br/>
하나의 흐름으로 연결해 관리할 수 있도록 만든 Connected Commerce 서비스입니다.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/services-6-orange?style=flat-square"/>
  <img src="https://img.shields.io/badge/RBAC-5%20roles-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/submodules-8-success?style=flat-square"/>
  <img src="https://img.shields.io/badge/deployment-GitOps-important?style=flat-square"/>
</p>

---

## Table of Contents

- [프로젝트 개요](#프로젝트-개요)
- [핵심 가치](#핵심-가치)
- [핵심 기능](#핵심-기능)
- [RBAC 5단계 권한 체계](#rbac-5단계-권한-체계)
- [서비스 흐름](#서비스-흐름)
- [MVP 범위](#mvp-범위)
- [Phase 2 예정 기능](#phase-2-예정-기능)
- [시스템 아키텍처](#시스템-아키텍처)
- [기술 스택](#기술-스택)
- [프로젝트 구조](#프로젝트-구조)
- [서비스 구성](#서비스-구성)
- [로컬 실행](#로컬-실행)
- [배포 흐름](#배포-흐름)
- [운영 시 유의사항](#운영-시-유의사항)

---

## 프로젝트 개요

| 항목 | 내용 |
| --- | --- |
| 프로젝트명 | CONK |
| 한 줄 소개 | 3PL 물류 운영사와 셀러를 위한 글로벌 풀필먼트 B2B SaaS 플랫폼 |
| 구성 | Vue 3 Frontend + 6개 Spring Boot 서비스 + Kubernetes |
| 운영 도메인 | [https://conk.site](https://conk.site) |
| API 도메인 | [https://api.conk.site](https://api.conk.site) |
| 저장소 역할 | 프론트엔드, 백엔드, 인프라 서브모듈을 묶는 루트 저장소 |

CONK는 수기와 엑셀 중심으로 흩어져 있던 창고 운영 흐름을 하나의 서비스 안으로 가져오는 데 집중합니다.  
입고, 적재, 재고, 주문, 출고, 배송, 정산까지 이어지는 흐름을 연결해서 3PL 운영사와 셀러가 같은 데이터를 보고 일할 수 있게 만드는 것이 목표입니다.

특히 아래와 같은 운영 문제를 줄이기 위해 설계했습니다.

- 다중 셀러 화물 관리의 복잡도
- 입고, 적재, 피킹, 패킹, 출고 과정의 비효율
- 창고 운영사와 셀러 사이의 정보 비대칭
- 판매 채널 수수료와 물류비를 반영한 마진 판단의 어려움

이 저장소는 프론트엔드, 6개의 백엔드 서비스, Kubernetes 매니페스트를 Git submodule로 묶어 관리하는 **루트 저장소**입니다.  
각 서비스는 독립적으로 개발 및 배포되며, 루트 저장소에서는 전체 구조 파악, 로컬 통합 실행, submodule 버전 관리를 담당합니다.

## 핵심 가치

### WMS 디지털화

ASN, 검수, Put-away, 재고 조회, 출고 처리까지 창고 운영 전 과정을 시스템화합니다.

### 풀필먼트 자동화

주문 수집, 재고 할당, 피킹 리스트 생성, 출고 확정 흐름을 표준화합니다.

### 셀러 가시성 강화

셀러가 본인 회사 기준 재고, 주문, 입고, 배송 흐름을 직접 확인할 수 있습니다.

### 수익성 의사결정 지원

마진 시뮬레이터를 통해 판매 전 예상 비용과 손익분기점을 빠르게 계산할 수 있습니다.

## 핵심 기능

### 플랫폼 및 테넌트 관리

- 3PL 업체 등록 및 `tenant_code` 발급
- 최초 총괄 관리자 초대 및 계정 활성화
- 업체 활성 및 비활성 관리, 데이터 격리

### 사용자 및 권한 관리

- `SYSTEM_ADMIN`, `MASTER_ADMIN`, `WH_MANAGER`, `WH_WORKER`, `SELLER` 5단계 RBAC
- 역할별 메뉴 노출 및 API 레벨 접근 제어
- 창고 관리자, 작업자, 셀러 담당자 초대 및 계정 상태 관리

### 창고 및 로케이션 관리

- 창고 등록 및 운영 정보 설정
- Zone-Rack-Bin 구조 로케이션 생성
- 창고별 운영 현황과 로케이션 상태 조회

### 입고 및 재고 관리

- ASN 등록 및 입고 예정 관리
- 바코드 기반 검수, 수량 불일치 확인, 불량 처리
- Put-away 위치 제안 및 적치 처리
- 셀러사별, SKU별 재고 현황 조회

### 주문 및 출고 관리

- 주문 수기 등록 및 엑셀 업로드
- 판매 채널 주문 연동 구조 지원
- 주문별 재고 할당, 피킹, 송장 발행, 출고 확정 처리

### 셀러 운영 지원

- 본인 회사 기준 재고, 주문, ASN 조회
- 최근 활동, 주문 상태, 재고 흐름 확인
- 대시보드 기반 운영 현황 확인

### 마진 시뮬레이터

- 판매 채널 수수료, 보관비, Pick & Pack, 라스트마일 비용 반영
- 부가 비용 파라미터를 반영한 수익성 계산
- 예상 순이익, 비용 상세, 손익분기점 수량 계산

### 실시간 알림 및 정산

- SSE 기반 실시간 알림 제공
- Redis Pub/Sub 기반 다중 인스턴스 알림 브로드캐스트
- 월별 정산 계산과 백필 배치 처리

## RBAC 5단계 권한 체계

> 기획 문서에서는 `3PL_ADMIN`이라는 표현을 사용하지만, 현재 프론트엔드와 서비스 코드에서는 동일한 역할을 `MASTER_ADMIN`으로 표현합니다.

| 역할 | 대상 | 주요 권한 |
| --- | --- | --- |
| `SYSTEM_ADMIN` | CONK 운영팀 | 3PL 업체 등록, 테넌트 활성화 및 비활성화, 플랫폼 관리 |
| `MASTER_ADMIN` | 창고 운영사 총괄 관리자 | 창고, 셀러사, 사용자, 단가, RBAC 관리 |
| `WH_MANAGER` | 창고 관리자 | ASN 처리, 검수 확인, 로케이션, 재고, 출고 운영 |
| `WH_WORKER` | 창고 작업자 | 검수, 적재, 피킹, 패킹, 현장 작업 수행 |
| `SELLER` | 셀러 및 화주 담당자 | 본인 재고, 주문, ASN 조회, 주문 등록, 마진 시뮬레이터 사용 |

## 서비스 흐름

1. `SYSTEM_ADMIN`이 3PL 업체를 등록하고 `tenant_code`를 발급합니다.
2. `MASTER_ADMIN`이 창고, 셀러 회사, 사용자, 단가표, 권한 설정을 구성합니다.
3. `SELLER`가 ASN과 주문을 등록하고 필요 시 판매 채널 연동을 연결합니다.
4. `WH_MANAGER`와 `WH_WORKER`가 입고 검수, 적재, 피킹, 패킹, 출고를 처리합니다.
5. `SELLER`는 재고, 주문, KPI, 마진 정보를 바탕으로 운영 상태와 수익성을 확인합니다.

## MVP 범위

- 다중 테넌트 기반 업체 등록 및 계정 초대
- 5단계 RBAC 권한 구조
- 창고 등록 및 Zone-Rack-Bin 로케이션 관리
- ASN 등록, 입고 검수, Put-away, 재고 조회
- 주문 등록, 벌크 업로드, 판매 채널 연동 기반 주문 처리
- 셀러 대시보드 및 마진 시뮬레이터

## Phase 2 예정 기능

- 채널 연동 고도화
- 로트 및 유통기한 관리
- 통계 및 리포트 확장
- 물류 운영 규칙과 자동화 로직 고도화

## 시스템 아키텍처

### 전체 구성

```text
User Browser
 ├─ Frontend
 │   └─ Vue 3 + Vite
 │       └─ S3 + CloudFront
 └─ API / SSE
     └─ api.conk.site
         └─ AWS ALB + Nginx Ingress
             ├─ member-service
             ├─ order-service
             ├─ wms-service
             ├─ integration-service
             ├─ notification-service
             └─ batch-service

Data / Messaging
 ├─ MariaDB
 ├─ Redis
 ├─ Kafka
 └─ WMS Read DB

External Integration
 ├─ EasyPost
 └─ Shopify API
```

### 계층별 설명

| 계층 | 구성 요소 | 역할 |
| --- | --- | --- |
| Client | User, Frontend | 사용자 화면 제공, API와 SSE 요청 발생 |
| Delivery | S3, CloudFront, `api.conk.site`, AWS ALB, Nginx Ingress | 정적 파일 배포, API 진입점, 라우팅, CORS 처리 |
| Application | `member-service`, `order-service`, `wms-service`, `integration-service`, `notification-service`, `batch-service` | 인증, 주문, 창고, 외부 연동, 알림, 정산 처리 |
| Data / Messaging | MariaDB, Redis, Kafka, WMS Read DB | 데이터 저장, 이벤트 전달, 캐시, 읽기 분리 |
| External | EasyPost, Shopify API | 배송 및 판매 채널 외부 연동 |

### 주요 처리 방식

- 보호된 API는 `member-service`의 인증 엔드포인트를 `auth_request`로 호출해 JWT를 검증하고, `X-User-Id`, `X-Tenant-Id`, `X-Role` 등의 헤더를 하위 서비스에 전달합니다.
- `notification-service`는 SSE로 실시간 알림을 전송하고, Redis Pub/Sub으로 다중 인스턴스 간 알림 상태를 맞춥니다.
- `order-service`, `wms-service`, `notification-service`, `batch-service`는 Kafka를 통해 이벤트를 주고받습니다.
- `batch-service`는 정산과 백필 작업을 담당하며 읽기 분리를 위해 `WMS Read DB`를 사용합니다.

## 기술 스택

### Design

<p>
  <img src="https://img.shields.io/badge/Figma-Design-F24E1E?style=for-the-badge&logo=figma&logoColor=white"/>
</p>

### Frontend

<p>
  <img src="https://img.shields.io/badge/Vue-3-4FC08D?style=for-the-badge&logo=vuedotjs&logoColor=white"/>
  <img src="https://img.shields.io/badge/Vite-7-646CFF?style=for-the-badge&logo=vite&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pinia-State%20Management-FFD859?style=for-the-badge&logo=vuedotjs&logoColor=black"/>
  <img src="https://img.shields.io/badge/Vue%20Router-Routing-4FC08D?style=for-the-badge&logo=vuedotjs&logoColor=white"/>
  <img src="https://img.shields.io/badge/Axios-HTTP%20Client-5A29E4?style=for-the-badge&logo=axios&logoColor=white"/>
  <img src="https://img.shields.io/badge/ApexCharts-Visualization-00E396?style=for-the-badge&logo=apexcharts&logoColor=white"/>
  <img src="https://img.shields.io/badge/Vitest-Testing-6E9F18?style=for-the-badge&logo=vitest&logoColor=white"/>
  <img src="https://img.shields.io/badge/JavaScript-ES2023-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black"/>
</p>

### Backend / Platform

<p>
  <img src="https://img.shields.io/badge/Java-21-007396?style=for-the-badge&logo=openjdk&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring%20Boot-3.5-6DB33F?style=for-the-badge&logo=springboot&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring%20Cloud-2025.0-6DB33F?style=for-the-badge&logo=spring&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring%20Security-Authentication-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white"/>
  <img src="https://img.shields.io/badge/JWT-Token%20Based-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring%20Data%20JPA-ORM-6DB33F?style=for-the-badge&logo=spring&logoColor=white"/>
  <img src="https://img.shields.io/badge/MyBatis-SQL%20Mapper-000000?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/OpenFeign-Service%20Call-6DB33F?style=for-the-badge&logo=spring&logoColor=white"/>
  <img src="https://img.shields.io/badge/Multi%20Tenant-Isolation-1D4ED8?style=for-the-badge"/>
</p>

### Data / Messaging

<p>
  <img src="https://img.shields.io/badge/MariaDB-10.11-003545?style=for-the-badge&logo=mariadb&logoColor=white"/>
  <img src="https://img.shields.io/badge/Redis-7-DC382D?style=for-the-badge&logo=redis&logoColor=white"/>
  <img src="https://img.shields.io/badge/Apache%20Kafka-Event%20Streaming-231F20?style=for-the-badge&logo=apachekafka&logoColor=white"/>
</p>

### Integration

<p>
  <img src="https://img.shields.io/badge/EasyPost-Shipping%20API-4C8BF5?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Shopify-API-95BF47?style=for-the-badge&logo=shopify&logoColor=white"/>
  <img src="https://img.shields.io/badge/XLSX-Bulk%20Upload-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white"/>
</p>

### Infrastructure / DevOps

<p>
  <img src="https://img.shields.io/badge/Docker-Container-2496ED?style=for-the-badge&logo=docker&logoColor=white"/>
  <img src="https://img.shields.io/badge/Docker%20Compose-Orchestration-2496ED?style=for-the-badge&logo=docker&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kubernetes-Orchestration-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white"/>
  <img src="https://img.shields.io/badge/Nginx%20Ingress-Routing-009639?style=for-the-badge&logo=nginx&logoColor=white"/>
  <img src="https://img.shields.io/badge/AWS%20ALB-Load%20Balancer-FF9900?style=for-the-badge&logo=amazonwebservices&logoColor=white"/>
  <img src="https://img.shields.io/badge/Amazon%20S3-Static%20Hosting-569A31?style=for-the-badge&logo=amazons3&logoColor=white"/>
  <img src="https://img.shields.io/badge/CloudFront-CDN-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white"/>
  <img src="https://img.shields.io/badge/ArgoCD-GitOps-EF7B4D?style=for-the-badge&logo=argo&logoColor=white"/>
  <img src="https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-2088FF?style=for-the-badge&logo=githubactions&logoColor=white"/>
  <img src="https://img.shields.io/badge/Docker%20Hub-Registry-2496ED?style=for-the-badge&logo=docker&logoColor=white"/>
</p>

## 프로젝트 구조

```text
be22-final-team1-project/
├── team1-frontend/                 # Vue 3 프론트엔드
├── team1-backend-member/           # 인증, 사용자, 권한, 업체/셀러 관리
├── team1-backend-order/            # 주문 등록, 벌크 업로드, 주문 상태 관리
├── team1-backend-wms/              # 창고, ASN, 재고, 출고, 작업 관리
├── team1-backend-integration/      # 채널 주문 연동, 송장 발행, 외부 API 연계
├── team1-backend-notification/     # 실시간 알림 및 unread count 관리
├── team1-backend-batch/            # 정산 배치 및 백필 작업
├── k8s-manifests/                  # Kubernetes 리소스 및 ArgoCD 배포 기준
├── docker-compose.yml              # 로컬 통합 실행 구성
├── docker-compose.db.yml           # DB 전용 보조 compose
├── nginx-gateway.conf              # 로컬 API 게이트웨이 설정
├── .env.example                    # 환경 변수 예시
└── README.md                       # 프로젝트 소개 문서
```

루트 저장소는 각 submodule의 SHA를 추적합니다.  
실제 기능 개발과 서비스별 설정은 각 submodule에서 진행되고, 이 저장소는 전체 프로젝트를 묶는 허브 역할을 합니다.

## 서비스 구성

| 서비스 | 역할 | 로컬 포트 |
| --- | --- | --- |
| `frontend` | 역할별 사용자 UI | `5173` |
| `api-gateway` | `/api/v1/*` 라우팅, CORS 처리, JWT 프록시 | `80` |
| `member-service` | 로그인, 토큰 재발급, 초대 메일, 권한 헤더 주입 | `8081` |
| `order-service` | 주문 등록, 벌크 업로드, 주문 조회 및 상태 관리 | `8082` |
| `wms-service` | ASN, 재고, 창고, 피킹, 출고 처리 | `8083` |
| `integration-service` | 채널 주문 동기화, 송장 발행, 외부 API 호출 | `8084` |
| `notification-service` | SSE 구독, 알림 조회, unread count | `8085` |
| `batch-service` | 정산 배치, 백필, 스냅샷 처리 | 외부 미노출 |
| `redis` | 알림 캐시 및 Pub/Sub | `7016` |
| `kafka` | 서비스 간 이벤트 브로커 | `7017` |

## 로컬 실행

### 요구 환경

- Node.js `^20.19.0 || >=22.12.0`
- Java 21
- Docker / Docker Compose

### 실행 순서

```bash
git clone --recurse-submodules <root-repository-url>
cd be22-final-team1-project
git submodule update --init --recursive
```

`.env.example`을 복사해 `.env.local` 파일을 만들고 필요한 값을 채웁니다.

주요 환경 변수:

- DB 접속 정보
- `JWT_SECRET`
- 메일 발송 계정
- `EASYPOST_API_KEY`
- `VITE_API_BASE_URL`
- `VITE_API_PREFIX`

준비가 끝나면 다음 명령으로 통합 실행할 수 있습니다.

```bash
docker compose --env-file .env.local up --build
```

### 로컬 접속 주소

| 대상 | 주소 |
| --- | --- |
| Frontend | [http://localhost:5173](http://localhost:5173) |
| API Gateway | [http://localhost](http://localhost) |
| Member Service | [http://localhost:8081](http://localhost:8081) |
| Order Service | [http://localhost:8082](http://localhost:8082) |
| WMS Service | [http://localhost:8083](http://localhost:8083) |
| Integration Service | [http://localhost:8084](http://localhost:8084) |
| Notification Service | [http://localhost:8085](http://localhost:8085) |
| Redis | `localhost:7016` |
| Kafka | `localhost:7017` |

참고:

- 브라우저 기준 실제 API 호출은 게이트웨이의 `/api/v1/*` 경로를 사용합니다.
- `batch-service`는 로컬 compose에서 외부 포트를 직접 열지 않으며 내부 배치 및 관리 목적 서비스로 동작합니다.
- 로컬 자산이 아직 정리되지 않은 환경이라면 DB 관련 bind mount 경로부터 먼저 확인하는 것이 좋습니다.

## 배포 흐름

### Frontend

- `team1-frontend` 변경 시 `frontend-ci-cd.yml`이 실행됩니다.
- `main` 브랜치에서는 프론트엔드 빌드 후 S3 동기화와 CloudFront 캐시 무효화를 수행합니다.
- 동시에 Docker 이미지를 Docker Hub로 푸시합니다.

### Backend

- 각 백엔드 서비스는 개별 workflow에서 공통 재사용 workflow인 `java-ci-cd.yml`을 호출합니다.
- `main` 브랜치 기준으로 Gradle 빌드 후 Docker Hub에 이미지를 푸시합니다.
- 이후 `k8s-manifests` 저장소의 `deployments.yaml` 이미지 태그를 갱신합니다.

### GitOps

- `k8s-manifests`는 실제 배포 기준 저장소입니다.
- `argocd-application.yaml` 기준으로 `main` 브랜치를 자동 동기화합니다.
- `prune`, `selfHeal` 옵션을 통해 Git 상태와 클러스터 상태를 최대한 일치시킵니다.

## 운영 시 유의사항

- `member-service`와 게이트웨이 구성이 인증의 기준점이므로 보호된 API 변경 시 헤더 계약을 함께 확인해야 합니다.
- `notification-service`는 SSE 특성상 프록시 버퍼링과 타임아웃 설정의 영향을 크게 받습니다.
- `wms-service`와 `batch-service`는 중복 처리와 스케줄 중복 실행을 피하기 위해 단일 replica 전략을 사용하는 구간이 있습니다.
- 민감 정보는 Git에 커밋하지 않고 환경 변수, Secret, 배포 환경 설정으로 주입해야 합니다.
