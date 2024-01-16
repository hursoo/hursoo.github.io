---
layout: single
title: "[23파이썬특강] 5강. 실전, 데이터 분석"
author_profile: false
toc : true
---

### 1. 개요
- 5강 ~ 8강에서는 본래 계획을 수정해서 교재 9장 이후는 일부만 살펴보고 역사 데이터를 분석하는 실제 사례를 중심으로 하고자 한다. 
- 5강에서는 교재 9장~11장의 일부 내용을 살펴본 후, 실제 사료 분석을 위해 필요한 파이썬 문법 및 판다스 문자열 처리를 집중적으로 익힌다.
- **교재 9장: '한국복지패널 데이터' 분석**에서는 샘플 데이터가 아닌 실제 데이터를 가지고 데이터 분석 절차를 진행해 보는 의의가 있다. 교재의 09-1은 기본 분석 절차를 다룬 것이고 09-2 ~ 09-9는 분석 패턴이 비슷하기 때문에 **09-1과 09-2만** 살펴볼 것이다.
- **교재 10장**: 이 교재의 텍스트 마이닝은 간략 검토. 형태소 분석기는 KoNLPy 대신 **[Kiwi(Korean Intelligent Word Identifier)](https://github.com/bab2min/kiwipiepy)**를 사용한다. 시각화로는 막대그래프만 살펴보고 워드 클라우드는 생략한다.
- **교재 11장**: 지도 시각화는 11-1만 살펴볼 것이다.

- 실습 코드
	- [**2023win_python_lec_05_basic.ipynb**](https://github.com/hursoo/2023_winter_python-lecture/blob/main/excise_code/2023win_python_lec_05.ipynb)
     
     
- 실습 데이터
    - [**Koweps_hpwc14_2019_beta2.sav**](https://github.com/youngwoos/Doit_Python) &rarr; Koweps_hpwc14_2019_beta2.md을 클릭하면 접속 링크가 나옴
    
    - [**speech_moon.txt**](https://github.com/youngwoos/Doit_Python/blob/main/Data/speech_moon.txt)
    - [**news_comment_BTS.csv**](https://github.com/youngwoos/Doit_Python/blob/main/Data/news_comment_BTS.csv)
    - [**SIG.geojson**](https://github.com/youngwoos/Doit_Python/blob/main/Data/SIG.geojson)
    - [**Population_SIG.csv**](https://github.com/youngwoos/Doit_Python/blob/main/Data/Population_SIG.csv)


### 2. '한국복지패널 데이터' 분석: 성별에 따라 월급이 다를까?
#### 2.1. 데이터 준비하기
- 전술한 실습 데이터 다운로드 &rarr; 워킹 디렉터리: 실습 데이터는 통계 분석 소프트웨어인 SPSS 전용 파일 
- 데이터: 2020년 발간. 6,331가구, 14,418명의 정보 수록. 14,418 * 830
#### 2.2. 패키지 설치 및 로드
- pyreadstat: 다양한 통계 분석 소프트웨어의 데이터 파일 불러올 수 있는 패키지
- 이외에 pandas, numpy, seaborn 등
#### 2.3. 데이터 불러오기
- pd.read_spss()
- 복사본 만들기: df1 = df.copy()
#### 2.4. 데이터 검토하기
```python
welfare               # 앞부분, 뒷부분 출력
welfare.shape         # 행, 열 개수 출력
welfare.info()        # 변수 속성 출력
welfare.describe()    # 요약 통계량
```
#### 2.5. 변수명 바꾸기
- 분석에 사용할 변수를 이해하기 쉬운 변수명으로 변경
- 코드북(codebook) 활용
#### 2.6. 데이터 분석 절차
- 1단계: 변수 검토 및 전처리: 변수 특징 파악 &rarr; 이상치, 결측치 정제 &rarr; 변수 값을 다루기 편하게 변환.  * 분석에 활용할 변수 각각 진행
- 2단계: 변수 간 관계 분석: 데이터를 요약한 표와, 데이터의 특징을 쉽게 이해할 수 있는 그래프 등을 작성 &rarr; 분석 결과를 해석


### 3. 유튜브 동영상을 통한 파이썬 문법 익히기


#### 리스트와 딕셔너리
- [**[1분 파이썬 - (16) 리스트 1 / 00:01:25]**(나도코딩, 2022-05-02)](https://www.youtube.com/watch?v=uxf4cTeonY4)
- [**[1분 파이썬 - (17) 리스트 2 / 00:01:23]**(나도코딩, 2022-05-03)](https://www.youtube.com/watch?v=KEhPKBpPJvI)
- [**[1분 파이썬 - (22) 딕셔너리 1 / 00:01:29]**(나도코딩, 2022-05-11)](https://www.youtube.com/watch?v=ZLp_Wg6VxfA&t=2s)
- [**[1분 파이썬 - (23) 딕셔너리 2 / 00:01:28]**(나도코딩, 2022-05-12)](https://www.youtube.com/watch?v=LV4IQnllYBA&t=15s)

#### 제어문: 조건문과 반복문
- [**[1분 파이썬 - (26) if 조건문 1 / 00:02:15]**(나도코딩, 2022-05-17)](https://www.youtube.com/watch?v=N92M3WaLbH0)
- [**[1분 파이썬 - (27) if 조건문 2 / 00:01:49]**(나도코딩, 2022-05-18)](https://www.youtube.com/watch?v=J9srd8Mfoyc)
- [**[1분 파이썬 - (29) for 반복문 / 00:01:44]**(나도코딩, 2022-05-20)](https://www.youtube.com/watch?v=uecZdRyiFNA)
- [**[1분 파이썬 - (31) for 활용 / 00:01:27]**(나도코딩, 2022-05-24)](https://www.youtube.com/watch?v=93_2E88rvDY)
- [**[1분 파이썬 - (36) 리스트 컴프리헨션 / 00:02:46]**(나도코딩, 2022-05-31)](https://www.youtube.com/watch?v=3wN0eVDhrvE)


#### 문자열 분리와 합치기: split, join
- [**[PYTHON-150 : 문자열(str)의 method-02, 문자열 분리, str.split / 00:05:48]**(EduAtoZ, 2020-05-10)](https://www.youtube.com/watch?v=BFCn_9BQ3fE)
- [**[PYTHON-151 : 문자열(str)의 method-03, 문자열 합치기, str.join / 00:03:15]**(EduAtoZ, 2020-05-10)](https://www.youtube.com/watch?v=vcut4hkExmA)
- [**[PYTHON-152 : 문자열(str) - split, join 실습 / 2020:05:10]**(EduAtoZ, 2020-05-10)](https://www.youtube.com/watch?v=ovwcIHnANSw&t=1s)


#### 함수
- [**[10강. 파이썬(Python) 기본 내장 함수의 이해 및 사용자 정의 함수 만들기 - 파이썬(Python) 입문자용 초급 / 00:06:12]**(동빈나, 2018-05-31)](https://www.youtube.com/watch?v=ufyLPag7eNs&list=PLRx0vPvlEmdD8u2rzxmQ-L97jHTHiiDdy&index=10)
- [**[파이썬 기초: 10-05-05 함수의 종류 : 람다 함수 / 00:15:02]**(박진수 SNU IDSLab, 2022-05-05)](https://www.youtube.com/watch?v=EQFgGsPFLWM)
- [**[파이썬 기초: 10-05-06 실습 : 일반 함수를 람다 함수로 변환 / 00:02:35]**(박진수 SNU IDSLab, 2022-05-05)](https://www.youtube.com/watch?v=-83gfX79NoQ&t=15s)
- [**[파이썬 기초: 10-05-07 실습 : 람다 함수 (1) / 00:02:29]**(박진수 SNU IDSLab, 2022-05-05)](https://www.youtube.com/watch?v=I6aqhRDM6lo)

#### 판다스 문자열 처리: 정규표현식, apply 함수, 중복데이터 삭제 등
- [**[PYTHON-re_11 : 정규식을 사용하여 문자열 대체 및 분리, sub, split / 00:03:19]**(EduAtoZ, 2021-01-10)](https://www.youtube.com/watch?v=x_H5XZmZN-)
- [**[1.2, 4/6 판다스로 텍스트 다루기, 파이썬 판다스 문자열 바꾸기 replace 와 str replace는 다른가? / 00:08:36]**(오늘코드, 2022-03-24)](https://www.youtube.com/watch?v=WrlovL32eEU&t=10s)
- [**[1.2, 5/6 판다스로 텍스트 다루기, 문자열 정규표현식으로 전처리하기, 문자길이와 단어개수, map apply / 00:14:36]**(오늘코드 , 2022-03-25)](https://www.youtube.com/watch?v=CdvYiCDKSWc)
- [**[Pandas 강의: apply 함수, 다양한 예제로 활용해보기 / 00:07:37]**(허민석, 2018-03-11)](https://www.youtube.com/watch?v=EHaDMTjCh5s&list=PLzyLx57OCtS4Ug4jgPru4da08PcFLfajj&index=11)
- [**[Pandas 강의: 중복 데이터 삭제하기 (drop duplicates) / 00:03:15]**(허민석, 2018-02-18)](https://www.youtube.com/watch?v=p6qEgqjv-H4&list=PLzyLx57OCtS4Ug4jgPru4da08PcFLfajj&index=8)

#### 머신러닝: 사이킷런으로 단어벡터 만들기
- [**[단어빈도와 Tf idf의 차이점은? / 00:04:27]**(해피AI, 2023-04-17)](https://www.youtube.com/watch?v=875HN8SrOfk)
- [**[2.2, 1/4, 단어 벡터 만들기: 사이킷런 문서의 단어 가방 만들기와 tfidf 가중치 적용하기 / 00:08:44]**(오늘코드, 2022-03-31)](https://www.youtube.com/watch?v=cRg4Eeo7K38)
- [**[2.2, 4/4, 단어 벡터 만들기: 예제 코퍼스에 TF IDF 가중치 적용하기 / 00:14:32]**(오늘코드, 2022-04-03)](https://www.youtube.com/watch?v=UVowQa5iY4w)

