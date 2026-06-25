# OOO교육기업 이벤트 마케팅 KPI AI Insight 분석

GA4 BigQuery 데이터를 기반으로 이벤트별 마케팅 KPI를 자동 집계하고,  
Vertex AI Gemini로 실행 액션 중심의 인사이트를 생성하는 마케팅 성과 분석 대시보드입니다.

단순 이벤트 특성 리포트가 아니라,  
**이벤트가 성과, 이벤트를 개선, 다음 액션**를 빠르게 판단이 가능합니다.

GA4 데이터 수집 → BigQuery KPI 집계 → 유저 군집 분석 → Vertex AI 인사이트 생성 → DATA Studio 시각화

---

## Preview
![대시보드 대표 화면](docs/images/01-main-dashboard.png)

- X축: 페이지 반응 또는 전환 관련 지표
- Y축: 구매전환 또는 참여전환 지표
- 버블 크기: 유입 또는 매출 규모
- 색상: 이벤트 성과 유형 또는 추천 액션
- 필터: 기간, 이벤트코드, 생성일자
  
---

## 프로젝트 요약

| 구분 | 내용 |
|---|---|
| 목적 | 이벤트별 마케팅 성과 진단 및 실행 액션 추천 자동화 |
| 데이터 | GA4 Export 기반 BigQuery 데이터 |
| 분석 단위 | 최근 3개월, 최근 1개월, 주차별 이벤트 성과 |
| 주요 지표 | 유입, 구매전환, 참여전환, 매출, 객단가 |
| 분석 방식 | 전체 이벤트 내 순위, 사분면 위치, 유저 군집 기반 성과 유형 분류 |
| AI 활용 | Vertex AI Gemini로 이벤트별 요약 및 실행 액션 자동 생성 |
| 시각화 | Looker Studio에서 기간, 이벤트 코드, 생성일 기준 필터링 |
| 자동화 | Cloud Run Jobs, Cloud Scheduler 기반 정기 실행 |

---

## 사용 기술

| 구분 | 사용 기술 |
|---|---|
| 데이터 소스 | GA4 Export |
| 데이터 웨어하우스 | BigQuery |
| 데이터 처리 | BigQuery SQL |
| AI 인사이트 생성 | Vertex AI Gemini |
| 자동화 실행 | Cloud Run Jobs |
| 스케줄링 | Cloud Scheduler |
| 시각화 | Data Studio |
| 컨테이너 | Docker, Artifact Registry |
| 언어 | Python, SQL |

---
## 3. 전체 시스템 구조

```mermaid
flowchart TD
    A["GA4 Raw Events"] --> B["EVENT KPI Query"]
    B --> C["KPI_EVENT"]

    A --> D["User Query"]
    D --> E["KPI_USER_CLASS"]
    E --> C

    C --> F["Prompt Query"]
    F --> G["Vertex AI Gemini"]
    G --> H["KPI_EVENT_AI_INSIGHTS"]

    C --> I["Data Studio Dashboard"]
    H --> I
```
