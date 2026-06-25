# OOO교육기업 이벤트 마케팅 KPI AI Insight 분석

GA4 BigQuery 데이터를 기반으로 이벤트별 마케팅 KPI를 자동 집계하고,  
Vertex AI Gemini로 실행 액션 중심의 인사이트를 생성하는 마케팅 성과 분석 대시보드입니다.

이 프로젝트는 단순 리포트가 아니라,  
**어떤 이벤트가 성과를 만들고 있는지, 어떤 이벤트를 개선해야 하는지, 다음 액션은 무엇인지**를 빠르게 판단하기 위해 구축했습니다.

GA4 데이터 수집 → BigQuery KPI 집계 → 유저 군집 분석 → Vertex AI 인사이트 생성 → DATA Studio 시각화

---

## Preview
![대시보드 대표 화면](docs/images/01-main-dashboard.png)

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
