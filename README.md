# CONK

**CONK**(CONnected commerce)는  
현지 창고를 보유한 3PL 및 물류 운영사의 **WMS/OMS 역량을 강화**하고,  
계약 셀러에게 **입고부터 출고, 배송 추적, 수익성 판단까지** 전 과정을 투명하게 제공하는  
**글로벌 풀필먼트 B2B SaaS 플랫폼**입니다.

수기·엑셀 중심으로 운영되는 창고 환경에서 반복되는

- 다중 셀러 화물 관리의 복잡도
- 입고, 적재, 피킹, 패킹, 출고 과정의 비효율
- 창고 운영사와 셀러 사이의 정보 비대칭
- 판매 채널 수수료와 물류비를 반영한 마진 판단의 어려움

을 줄이는 것을 목표로 합니다.

---

## 핵심 가치

- **WMS 디지털화**  
  ASN, 검수, Put-away, 재고 조회, 출고 처리까지 창고 운영 전 과정을 시스템화합니다.

- **풀필먼트 자동화**  
  주문 수집, 재고 할당, 피킹 리스트 생성, 출고 확정 흐름을 표준화합니다.

- **셀러 가시성 강화**  
  셀러가 본인 회사 기준 재고, 주문, 입고, 배송 흐름을 직접 확인할 수 있습니다.

- **수익성 의사결정 지원**  
  마진 시뮬레이터를 통해 판매 전 예상 비용과 손익분기점을 빠르게 계산할 수 있습니다.

---

## 핵심 기능

- **플랫폼 및 테넌트 관리**
  - 3PL 업체 등록 및 `tenant_code` 발급
  - 최초 총괄 관리자 초대 및 계정 활성화
  - 업체 활성/비활성 관리 및 데이터 격리

- **사용자 및 권한 관리**
  - `SYSTEM_ADMIN`, `MASTER_ADMIN`, `WH_MANAGER`, `WH_WORKER`, `SELLER` 5단계 RBAC
  - 역할별 메뉴 노출 및 API 레벨 접근 제어
  - 창고 관리자, 작업자, 셀러 담당자 초대 및 계정 상태 관리

- **창고 및 로케이션 관리**
  - 창고 등록 및 운영 정보 설정
  - Zone-Rack-Bin 구조 로케이션 생성
  - 로케이션 가용률 및 창고별 운영 현황 조회

- **입고 및 재고 관리**
  - ASN 등록 및 입고 예정 관리
  - 바코드 기반 검수, 수량 불일치 확인, 불량 사진 첨부
  - Put-away 위치 자동 제안
  - 셀러사별/SKU별 재고 현황 및 Safety Stock 알림

- **주문 및 출고 관리**
  - 주문 수기 등록, 엑셀 업로드
  - Amazon SP-API 기반 주문 자동 수집
  - 주문별 재고 할당, 피킹 리스트 생성, 패킹 및 출고 확정

- **셀러 운영 지원**
  - 본인 회사 기준 재고/주문/ASN 조회
  - 최근 활동, 주문 상태, 재고 변동 이력 확인
  - 출고 창고 선택 및 재입고 흐름 연결

- **마진 시뮬레이터**
  - 판매 채널 수수료, 보관비, Pick & Pack, 라스트마일 비용 반영
  - 해상/항공 수입 부가비용 파라미터 반영
  - 예상 순이익, 비용 상세, 손익분기점 수량 계산

---

## RBAC 5단계 권한 체계

> 기획서에서는 `3PL_ADMIN` 용어를 사용하고, 현재 프론트엔드 코드에서는 같은 역할을 `MASTER_ADMIN`으로 표현합니다.

| 역할 | 대상 | 주요 권한 |
|:--|:--|:--|
| `SYSTEM_ADMIN` | CONK 운영팀 | 3PL 업체 등록, 테넌트 활성화/비활성화, 플랫폼 관리 |
| `MASTER_ADMIN` | 창고 운영사 총괄 관리자 | 창고/셀러사/사용자/단가/RBAC 관리 |
| `WH_MANAGER` | 창고 관리자 | ASN 처리, 검수 확인, 로케이션/재고/출고 운영 |
| `WH_WORKER` | 창고 작업자 | 검수, 적재, 피킹, 패킹, 현장 작업 수행 |
| `SELLER` | 셀러/화주 담당자 | 본인 재고/주문/ASN 조회, 주문 등록, 마진 시뮬레이터 사용 |

---

## 서비스 흐름

1. `SYSTEM_ADMIN`이 3PL 업체를 등록하고 `tenant_code`를 발급합니다.
2. `MASTER_ADMIN`이 창고, 셀러 회사, 사용자, 단가표, 권한 설정을 구성합니다.
3. `SELLER`가 ASN과 주문을 등록하고, 필요 시 Amazon 주문 연동을 연결합니다.
4. `WH_MANAGER`와 `WH_WORKER`가 입고 검수, 적재, 피킹, 패킹, 출고를 처리합니다.
5. `SELLER`는 재고/주문/KPI/마진 정보를 바탕으로 운영 상태와 수익성을 확인합니다.

---

## MVP 범위

- 다중 테넌트 기반 업체 등록 및 계정 초대
- 5단계 RBAC 권한 구조
- 창고 등록 및 Zone-Rack-Bin 로케이션 관리
- ASN 등록, 입고 검수, Put-away, 재고 조회
- 주문 등록, Amazon SP-API 주문 수집, 출고 처리
- 셀러 대시보드 및 마진 시뮬레이터

**Phase 2 예정 기능**

- Shopify 주문 자동 연동
- 로트/유통기한 관리
- 고도화된 통계/리포트 및 확장 물류 로직

---

## 시스템 아키텍처

아키텍처 구조도를 자세히 보려면 [여기]()를 클릭하세요. <br>

<details>
  <summary>시스템 아키텍처 구조도</summary>

  
</details>

---

## 기술 스택

### Design

![Figma](https://img.shields.io/badge/Figma-000000?style=for-the-badge&logo=figma&logoColor=white)

### Frontend

![Vue.js](https://img.shields.io/badge/Vue.js-35495E?style=for-the-badge&logo=vue.js&logoColor=4FC08D)
![Pinia](https://img.shields.io/badge/Pinia-FFD54F?style=for-the-badge&logo=vue.js&logoColor=black)
![Axios](https://img.shields.io/badge/Axios-5A29E4?style=for-the-badge)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![Vitest](https://img.shields.io/badge/Vitest-6E9F18?style=for-the-badge&logo=vitest&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

### Backend / Platform

![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge)
![RBAC](https://img.shields.io/badge/RBAC-2F5D62?style=for-the-badge)
![Multi Tenant](https://img.shields.io/badge/Multi--Tenant-1D4ED8?style=for-the-badge)

### Integration

![Amazon SP-API](https://img.shields.io/badge/Amazon_SP--API-FF9900?style=for-the-badge&logo=amazon&logoColor=white)
![XLSX](https://img.shields.io/badge/XLSX-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)

### Collaboration

![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)

---

## 기획 & 설계 문서

### 프로젝트 기획서

프로젝트 기획서를 자세히 보려면 [여기](https://docs.google.com/document/d/1bQ7wX01OydhQRKkWQhwKwiPuiOlo4mM3/edit)를 클릭하세요. <br>

### WBS

  WBS를 자세히 보려면 [여기](https://docs.google.com/spreadsheets/d/1CvZBzU7ZUd2ZnMKb0mKBaGY_xLiCozGYOC20BCKHqf0/edit?gid=973268466#gid=973268466)를 클릭하세요. <br>

  <details>
    <summary>WBS</summary>

  </details>


    

### 요구사항 명세서

  요구사항명세서를 자세히 보려면 [여기](https://docs.google.com/spreadsheets/d/1f1WFkpN6R4Dedb-mRi5JRoFwjD6p1I7M/edit?gid=1286504416#gid=1286504416)를 클릭하세요. <br>

  <details>
    <summary>요구사항 명세서</summary>

  </details>

### API 명세서

  <details>
    <summary>API 명세서</summary>

  </details>

### ERD **(Entity Relationship Diagram)**

  ERD를 자세히 보려면 [여기](https://www.erdcloud.com/d/apypTYheQFsKPpDTd)를 클릭하세요. <br>

  <details>
    <summary>ERD</summary>
  </details>

### 백엔드 단위 테스트

  <details>
    <summary>백엔드 단위 테스트</summary>
  </details>

### 화면 설계서

  화면설계서를 자세히 보려면 [여기](https://www.figma.com/design/HFMDA9EPpTDL3csGThnTLl/CONK-%ED%99%94%EB%A9%B4%EC%84%A4%EA%B3%84%EC%84%9C?node-id=0-1&t=8RK3urXY6dMhA19e-1)를 클릭하세요. <br>

### 프론트 단위 테스트

  프론트 단위 테스트 결과서를 자세히 보려면 [여기](https://docs.google.com/spreadsheets/d/1uHTF6NGskmzIJVpBpEI3M_vGwLvJeC_lRElNUn7qcXA/edit?gid=1447356514#gid=1447356514)를 클릭하세요.

### 통합 테스트 결과서

  통합테스트 결과서를 자세히 보려면 [여기]()를 클릭하세요.

---
## 배포 문서

### CI/CD 계획서

  CI/CD 계획서를 자세히 보려면 [여기]()를 클릭하세요. <br>

---

## 로컬 실행

### 요구 환경

- Node.js `^20.19.0 || >=22.12.0`
- npm

### 실행

```bash
npm install
npm run dev
npm run mock
```



---
>>>>>>> ecd68f0ea57b57997a45c901e7f59d8e035c5305
