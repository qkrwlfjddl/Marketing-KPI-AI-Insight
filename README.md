<div align="center">

# Event Intelligence

### GA4 행동 로그 기반 이벤트 마케팅 의사결정 시스템

**고객 행동 분석 · 이벤트 성과 진단 · 생성형 AI 액션 제안**

<p>
  <img src="https://img.shields.io/badge/GA4-Analytics-E37400?style=flat-square&logo=googleanalytics&logoColor=white">
  <img src="https://img.shields.io/badge/BigQuery-Data%20Warehouse-669DF6?style=flat-square&logo=googlebigquery&logoColor=white">
  <img src="https://img.shields.io/badge/BigQuery%20ML-K--Means-4285F4?style=flat-square&logo=googlecloud&logoColor=white">
  <img src="https://img.shields.io/badge/Vertex%20AI-Gemini-8E75B2?style=flat-square&logo=googlecloud&logoColor=white">
  <img src="https://img.shields.io/badge/Looker%20Studio-Dashboard-4285F4?style=flat-square&logo=looker&logoColor=white">
</p>

</div>

---

## 프로젝트 개요

기존 이벤트 리포트는 유입·매출·전환율을 보여줬지만,  
**어떤 이벤트를 확대하고 무엇을 개선해야 하는지**는 담당자가 다시 분석해야 했습니다.

이 프로젝트는 GA4 로그에서 고객 행동과 이벤트 특성을 각각 만들고 결합해 이벤트의 역할과 성과를 진단한 뒤, AI가 근거와 다음 액션을 설명하도록 설계했습니다.

| 기존 리포트 | 분석 구조 개선 | AI 의사결정 지원 |
|:---:|:---:|:---:|
| 유입·매출·전환을 개별 확인 | 고객 행동과 이벤트 성과를 결합 | 근거·원인·액션을 자연어로 제공 |
| **숫자의 의미를 사람이 재분석** | **이벤트의 역할과 고객 맥락 진단** | **검증 가능한 다음 액션 제안** |

이를 통해 마케팅 담당자는 여러 보고서를 오가며 숫자를 다시 해석하지 않고, 한 화면에서 다음 질문에 답할 수 있습니다.

- 지금 확대할 이벤트는 무엇인가?
- 유입은 많은데 구매가 낮은 이유는 무엇인가?
- 각 이벤트에는 어떤 성향의 고객이 들어오는가?
- 개선 후 어떤 KPI를 확인해야 하는가?

### 설계 기준

- 고객군은 분기별, 이벤트 KPI는 일별로 갱신해 안정성과 최신성을 함께 유지
- 구매 전환과 참여 전환을 분리해 이벤트의 퍼널 역할을 구분
- 정확한 계산은 SQL, 비즈니스 해석은 AI가 담당
- 개인 데이터 대신 이벤트별 고객군 구성비만 최종 화면에 제공
- 고정 기준보다 같은 기간 전체 이벤트 안에서의 상대 위치를 평가

[구축 과정과 기술적 의사결정 보기 →](docs/implementation.md)

---

## Before / After

### 기존 화면

<p align="center">
  <img src="docs/images/orign_event.png" alt="기존 이벤트 성과 조회 화면" width="50%">
</p>

유입, 매출, 전환율을 각각 확인해야 해 이벤트 간 비교와 개선 우선순위 선정이 어려웠습니다.

### 개선 화면

<p align="center">
  <img src="docs/images/signup_event.png" alt="구축 후 유입 중심 이벤트 분석 대시보드" width="82%">
</p>

UX 반응과 전환율을 사분면으로 비교하고, 버블 크기와 색상으로 이벤트 규모·성과 유형·추천 액션을 함께 확인합니다.

---

## 분석 구조

```mermaid
flowchart LR
    A["GA4<br/>원천 로그"] --> B["고객 행동<br/>피처"]
    A --> C["이벤트 성과<br/>피처"]
    B --> D["K-Means<br/>고객군"]
    C --> E["UX·전환·매출<br/>상대 평가"]
    D --> F["고객 × 이벤트<br/>통합 피처"]
    E --> F
    F --> G["Vertex AI<br/>해석·액션"]
    F --> H["Looker Studio"]
    G --> H
```

### 01. 고객 행동

클릭·체류·스크롤·경로·구매 행동을 세션 단위로 가공하고, BigQuery ML K-Means로 행동 기반 고객군을 생성했습니다.

### 02. 이벤트 성과

3개월·1개월·주차별로 UX Score, 구매·참여 전환율, 매출과 상대 순위를 계산했습니다.

### 03. 데이터 결합

고객군을 이벤트 방문 데이터에 다시 연결해 이벤트별 고객 구성과 성과를 하나의 피처로 만들었습니다.

### 04. AI 해석

SQL이 계산한 피처를 구조화된 프롬프트로 전달해 **관찰 → 원인 가설 → 실행 액션 → 확인 KPI** 순서의 인사이트를 생성했습니다.

[고객 피처부터 AI 프롬프트까지 전체 방법론 보기 →](docs/methodology.md)

[전체 시스템과 데이터 흐름 보기 →](docs/architecture.md)

---

## 대시보드

### 매출 관점

<p align="center">
  <img src="docs/images/price_event.png" alt="매출 중심 이벤트 분석 대시보드" width="82%">
</p>

매출과 구매자당 평균 매출을 기준으로 이벤트의 수익성과 확장 가능성을 비교합니다.

### 이벤트 비교

<p align="center">
  <img src="docs/images/event_group_DS.png" alt="이벤트 성과 그룹 비교 화면" width="52%">
</p>

기간, 이벤트 코드, 유입·매출 순위 조건을 적용해 비교 대상을 좁히고 이벤트의 상대적 위치를 확인합니다.

---

## 프로젝트 결과

이 프로젝트를 통해 이벤트 리포트를 **현황 조회 화면**에서 **실행 우선순위를 제안하는 분석 제품**으로 확장했습니다.

- 고객 행동과 이벤트 성과를 연결해 전환 결과의 배경을 설명
- 구매형·탐색형 이벤트를 서로 다른 기준으로 평가
- 장기·단기·주차 흐름을 함께 비교해 성과 변화 감지
- SQL 기반의 재현 가능한 계산과 AI 기반 자연어 해석을 결합
- 분석 결과를 실무자가 바로 사용할 수 있는 대시보드로 제공

### 조직에 제공할 수 있는 가치

이 프로젝트에서 얻은 가장 큰 경험은 특정 모델을 사용하는 방법보다,  
**흩어진 데이터를 실무자의 판단 과정에 맞는 제품으로 구조화하는 방법**입니다.

새로운 조직에서도 다음과 같은 방식으로 기여할 수 있습니다.

- 반복적으로 사람이 해석하는 보고 과정을 데이터 모델과 자동화 구조로 전환
- 고객 행동과 매출 데이터를 연결해 마케팅 우선순위와 실험 가설 제안
- 생성형 AI의 역할을 명확히 분리해 신뢰할 수 있는 AI 분석 기능 설계
- 분석가뿐 아니라 현업 담당자도 사용할 수 있는 화면과 업무 흐름 구축

> **데이터를 보여주는 것에서 끝내지 않고, 다음 행동을 결정할 수 있는 구조를 만듭니다.**

<sub>OOO 교육기업 데이터를 기반으로 구현한 프로젝트입니다. 공개 문서에서는 기업명, 프로젝트 ID, 사업부 코드와 사용자 식별 정보를 비식별화했습니다.</sub>

