---
title: 2주차. 챗봇 프로젝트
---

# SSAFY Start Camp 챗봇 퀘스트 ([original repo link](https://github.com/CoaLee/hotword))
서울_5_이용재, https://github.com/CoaLee/hotword
## 1. 스펙(Specification)
- **용도**: 뉴스 분야(정치, IT, 연예..) 또는 특정 키워드(손흥민, 삼성, ...)를 검색했을 때 연관된 단어들 보여준다.
- **기능**:
  1. 다이얼로그 플로우로 Query 분석
  2. 뉴스 사이트(다음 뉴스/조선일보)를 통해 최근 기사 크롤링 
  3. 기사의 단어들을 세어서 단어구름(wordcloud) 생성
- **예상 유저**: 빠르게 트렌드를 알고 싶은 사람, 뉴스에 관심이 많은 사람
- **팀원별 역할 분담**: 구조 만들기 (이용재) / 크롤링(지창규) / 연산 및 단어구름 생성(박준호)

|**뉴스 카테고리 검색**|**키워드 검색**|
|---|---|
|다음 뉴스 카테고리: 다음 뉴스에서 미리 크롤링한 데이터 활용|그 외 검색어: 언론 사이트에 검색하여 크롤링|

## 2. 회고(Retrospective)
### 어려웠던 점
- 크롤링: 검색어에 대해 기사 내용을 가져오는 경우 Python에서 한글로 인식이 안되어 인코딩 불가 --> `soup = Beautifulsoup(r.content.decode('euc-kr', 'replace'))` 으로 해결
- 검색: 뉴스 내용에서 필요한 키워드를 추출할 때, 한글 조사를 해결해야 하는 어려움이 있었음 --> KoNLPy 라이브러리를 통해 해결
- 쿼리 분석: DialogFlow에서 인텐트를 각 카테고리마다 생성해야 할 뻔 했다가 --> 하나의 인텐트와 Entity를 이용해서 키워드 및 카테고리를 전달하여 해결

## 3. 보완 계획(Feedback)
### 주요한 기능
- 특정 인물을 물어보면 해당 인물의 SNS를 크롤링하여 사용한 단어 빈도로 단어구름 그리기
- 특정 가수를 물어보면 가수의 가사를 크롤링하여 단어구름 그리기 

### 기능 심화
- 크롤링 자동화
- 크롤링 대상 사이트 늘리기
- wordcloud 마스킹 활용(사랑을 검색하면 하트 모양 위에 단어가 그려지도록)
  - 단어 이미지 검색
  - 마스킹 이미지로 변환
  - 활용하기
- DialogFlow로 쿼리를 더 잘 이해할 수 있도록 학습시키기
- DialogFlow가 다양한 질의를 이해할 수 있도록 하기


## 4. Component: 
### Framework, API
- Python Flask (Server)
- Slack API (Bot)
- DialogFlow (Query Interpretation)

### Library
- BeautifulSoup4, Requests (Crawling)
- Wordcloud, Matplotlib (Wordcloud Creation)
- KoNLPy (Hangul Processing, Vocab Extraction)

### etc
- Ngrok (Server Webhook)
- Slacker (Slack Interaction)

