# Restaurant Topic Modeling

> 2022-2학기 국민대학교 **텍스트 데이터 분석** 학부 수업의 개인 프로젝트입니다. 네이버 VIEW · 다이닝코드 · 망고플레이트 · 서울시 공공데이터를 동적 크롤링해 **국민대 / 정릉시장 주변 맛집 리뷰** 텍스트 코퍼스를 구축한 뒤, 형태소 분석과 LSA / LDA 토픽 모델링을 적용해 동네 맛집을 묶어보는 흐름을 정리했습니다.

## Overview

| 항목 | 내용 |
| --- | --- |
| 수업 | 텍스트 데이터 분석 (국민대학교 학부 강의) |
| 기간 | 2022.09 ~ 2022.12 |
| 형태 | 개인 프로젝트 |
| 주제 | 국민대 / 정릉시장 주변 맛집 리뷰 토픽 모델링 |
| 데이터 | 네이버 VIEW, 다이닝코드, 망고플레이트, 서울시 공공데이터(성북구 일반음식점 인허가) |
| 크롤링 | Selenium 동적 크롤링 (BeautifulSoup 정적 보조) |
| 분석 | KoNLPy 형태소 분석 (Komoran/Kkma/Mecab/Twitter 비교) + LSA + LDA |

## Approach

### 데이터 수집
- 네이버 **VIEW** 검색 (`정릉시장맛집`, `정릉맛집`, `국민대맛집`) — 통합 검색 결과의 제목 + 미리보기 3줄.
- **다이닝코드** / **망고플레이트** — 정릉/국민대 검색 후 음식점 페이지 전체 크롤링.
- **서울시 공공데이터** — 성북구 일반음식점 인허가 정보를 음식점명 빈도 보강용으로 사용.
- 음식점이 자주 폐업/리브랜딩되는 도메인 특성상 **동적 크롤링(Selenium + ChromeDriver)** 으로 통일.

### 전처리 / 형태소 분석
- 영화 제목·음식점명 같은 **공백 포함 고유명사** 가 많아 `Komoran` 을 1차로 사용.
- 비교용으로 `Hannanum`, `Kkma`, `Twitter`, `Mecab` 도 같이 돌려 결과 차이를 보고서에 기록.
- 불용어 사전 (`Data_stop_word`) + 빈도 기반 필터로 노이즈 제거.

### 토픽 모델링
- LSA (TruncatedSVD) → 빠른 baseline 으로 주요 축 확인.
- LDA (gensim) → 토픽 수 후보별 perplexity / coherence 비교 후 확정.
- 토픽별 상위 키워드 + 음식점 매핑을 wordcloud / matplotlib / seaborn 으로 시각화.

## Repository Structure

```text
.
├── notebooks/
│   ├── 01_crawling_and_preprocessing.ipynb    # 4개 소스 크롤링 + 형태소 분석기 비교 + 빈도 분석
│   └── 02_topic_modeling.ipynb                # LSA + LDA + 시각화
├── reports/
│   ├── 01_research_proposal.pdf               # 연구배경 / 데이터 선택 사유 / 형태소 분석기 설명
│   ├── 02_topic_modeling_results.pdf          # 토픽 모델링 결과 보고서
│   └── presentation_video.mp4                 # 발표 영상 (~22MB, 본인 내레이션)
├── .gitignore
└── README.md
```

## Public Scope

이 저장소는 포트폴리오 공개용으로 정리한 버전입니다.

- 크롤링 raw 데이터 (`contents.xlsx`, `Data_stop_word`, 다운로드된 JSON/CSV) 와 모델 산출물은 포함하지 않습니다 (`.gitignore` 로 차단).
- 노트북 출력 결과와 실행 메타데이터는 제거했습니다.
- 원본 파일명에 포함되어 있던 `Web_crawling+LSA,LDA-Part-01/02` 식의 이름은 영문 snake_case 로 통일했습니다.
- 발표 영상(`reports/presentation_video.mp4`) 은 본인 음성 내레이션이 포함된 22MB 파일이라 직접 커밋했습니다 — GitHub LFS 가 필요할 정도 크기는 아니지만, 추후 영상이 늘어나면 LFS 전환을 고려하세요.
