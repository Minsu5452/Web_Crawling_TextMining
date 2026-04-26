# 국민대·정릉시장 맛집 토픽 모델링

국민대학교 텍스트 데이터 분석 수업에서 국민대·정릉시장 주변 맛집 리뷰를 수집하고 LSA/LDA 토픽 모델링을 수행한 개인 프로젝트입니다.

## 개요

| 항목 | 내용 |
| --- | --- |
| 수업 | 텍스트 데이터 분석 |
| 기간 | 2022.09 - 2022.12 |
| 형태 | 개인 프로젝트 |
| 데이터 | 네이버 VIEW, 다이닝코드, 망고플레이트, 서울시 공공데이터 |
| 분석 | Selenium crawling, KoNLPy, LSA, LDA |

## 접근

- 네이버 VIEW, 다이닝코드, 망고플레이트, 서울시 성북구 음식점 데이터를 수집했습니다.
- Selenium 기반 동적 크롤링을 사용하고 BeautifulSoup을 보조적으로 활용했습니다.
- Komoran, Hannanum, Kkma, Twitter, Mecab 형태소 분석 결과를 비교했습니다.
- 불용어와 빈도 기준 필터링 후 LSA와 LDA로 토픽을 추출했습니다.
- 토픽별 키워드와 음식점 매핑을 시각화했습니다.

## 저장소 구성

```text
.
├── notebooks/
│   ├── 01_crawling_and_preprocessing.ipynb
│   └── 02_topic_modeling.ipynb
└── reports/
    ├── 01_research_proposal.pdf
    ├── 02_topic_modeling_results.pdf
    └── presentation_video.mp4
```

## 공개 범위

크롤링 원본 데이터, 불용어 파일, 중간 산출물, 모델 산출물은 포함하지 않았습니다. 노트북 출력과 로컬 경로를 정리했습니다.
