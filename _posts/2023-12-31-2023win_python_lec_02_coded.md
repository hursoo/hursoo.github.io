---
layout: single
title: "[23파이썬특강] 2강. 데이터 프레임과 분석 기초(코드 검색)_1"
author_profile: false
toc : true
---

<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3; 
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>


# <span style="color:blue; font-weight:bold;">2강. 데이터 프레임과 분석 기초</span>

- 둘째마당 (04-05)

- pp.074-130 (57쪽)



```python
# 그래프 해상도 설정
import matplotlib.pyplot as plt
plt.rcParams.update({'figure.dpi' : '100'})
%config InlineBackend.figure_format = 'retina'
```

# 04. 데이터 프레임의 세계로


## 04-1. 데이터 프레임 이해하기(77-80쪽)

- 데이터는 어떻게 생겼나?


- '열'은 속성(변수), '행'은 한 사람[혹은 한 단위]의 정보

- 한 사람의 정보는 가로 한 줄에 나열

- 데이터가 '크다' = 행 또는 열이 '많다'

- 행 보다 '열'이 많은 것이 더 중요

- 빅데이터보다 다양한 데이터가 더 중요


## 04-2. 데이터 프레임 만들기(81-84쪽)


### [Do it! 실습] 데이터 입력해 데이터 프레임 만들기(81쪽)



```python
import pandas as pd
```


```python
# '딕셔너리' 형식('{}')의 데이터를 이용해서 만들기
## -> 딕셔너리에 관하여는 교재 '17-5. 딕셔너리'(418-421쪽) 참조
# DataFrame -> D, F가 대문자

```

### [Do it! 실습] 데이터 프레임으로 분석하기(82쪽)


#### 특정 변수의 값 추출하기



```python
```

#### 변수의 값으로 합계 구하기



```python
# 영어 점수 합계
```


```python
# 수학 점수 합계
```

#### 변수의 값으로 평균 구하기



```python
# 영어 점수 평균
```


```python
# 수학 점수 평균
```

### [개인 실습] 혼자서 해보기(84쪽)


### Q1

다음 표의 내용을 데이터 프레임으로 만들어 출력해 보세요

| 제품  | 가격  | 판매량 |

|:-----:|:-----:|:------:|

| 사과  | 1800  |   24   |

| 딸기  | 1500  |   38   |

| 수박  | 3000  |   13   |


##### A1



```python
# 변수 fruit 사용
```

### Q2

- 앞에서 만든 데이터 프레임을 이용해 과일의 가격 평균과 판매량 평균을 구하라


##### A2



```python
# 가격 평균: 변수 fruit_average_price 사용
```


```python
# 판매량 평균: 변수 fruit_average_quantity 사용
```

## 04-3. 외부 데이터 이용하기(85-92)

- 축적된 시험 성적 데이터를 불러오자!


### [Do it! 실습] 엑셀 파일 불러오기(85쪽)


#### 엑셀 파일 살펴보기

- 깃허브에서 다운로드 (-> 교재 14쪽 참고)


#### 워킹 디렉토리에 엑셀 파일 삽입하기

- excel_exam.xlsx



```python
import pandas as pd

# 변수 df_exam 사용
```


```python
# 영어 점수 평균
```


```python
# 과학 점수 평균
```


```python
# len 사용한 평균 구하기

x = [1, 2, 3, 4, 5]
len(x)
```

<pre>
5
</pre>

```python
df = pd.DataFrame({'a':[1,2,3],
                   'b':[4,5,6]})
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



```python
len(df)
```

<pre>
3
</pre>

```python
# df_exam 개수
```


```python
# 영어 점수 평균 구하기 (len 사용)
```


```python
# 과학 점수 평균 구하기 (len 사용)
```

### 엑셀 파일의 첫 번째 행이 변수명이 아니라면?



```python
# excel_exam_novar.xlsx 불러오기. 변수 df_exam_novar 사용
```


```python
# 첫 번째 행이 변수명이 아님을 알려주는 코드: header=None -- 변수명은 df_exam_novar로
```

### [Do it! 실습] CSV 파일 불러오기(90쪽)



```python
# CSV 파일 'exam.csv' 불러오기. 변수명은 df_csv_exam로
```

### [Do it! 실습] 데이터 프레임을 CSV 파일로 저장하기(91쪽)



```python
# 저장하기 위한 데이터 프레임 만들기

df_midterm = pd.DataFrame({'english':[90, 80, 60, 70],
                           'math':[50, 60, 100, 20],
                           'nclass':[1, 1, 2, 2]})
df_midterm
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>english</th>
      <th>math</th>
      <th>nclass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>90</td>
      <td>50</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>60</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>60</td>
      <td>100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>70</td>
      <td>20</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



```python
# df_midterm을 output_newdata.csv라는 파일명으로 저장하기 (인덱스 번호 포함/제외하기): index=True/False
```


```python
# 다시 불러오기: output_newdata.csv를 불러와서 변수 reload에 담기
```

# 05. 데이터 분석 기초


## 05-1. 데이터 파악하기(99-106쪽)

- head(), tail(), shape, info(), describe()



```python
# exam.csv 불러와서 변수 exam에 담기
import pandas as pd
```


```python
# 앞부분 5개 행 출력
```


```python
# 앞부분 10개 행 출력
```


```python
# 뒷부분 5개 행 출력
```


```python
# 뒷부분 10개 행 출력
```


```python
# 행, 열 개수출력
```


```python
# 변수 속성 출력
```


```python
# 요약 통계량 출력
```


```python
# mpg.csv 데이터 불러와서 변수 mpg에 담기
'''
cf) mpg : mpg(Mile Per Gallon) 데이터는 
미국 환경 보호국(US Environmental Protection Agency)에서 공개한 자료로, 
1999~2008년 사이 미국에서 출시된 자동차 234종의 연비 관련 정보를 담고 있다.
https://m.blog.naver.com/eunha4685/221496862666
'''
```

<pre>
'\ncf) mpg : mpg(Mile Per Gallon) 데이터는 \n미국 환경 보호국(US Environmental Protection Agency)에서 공개한 자료로, \n1999~2008년 사이 미국에서 출시된 자동차 234종의 연비 관련 정보를 담고 있다.\nhttps://m.blog.naver.com/eunha4685/221496862666\n'
</pre>

```python
# mpg 앞부분 5개 행 출력
```


```python
# mpg 뒷부분 5개 행 출력
```


```python
# mpg 행과 열 개수 출력
```


```python
# mpg 변수 속성 출력
```


```python
# mpg 요약 통계량 출력 (숫자로 된 변수만)
```


```python
# mpg 요약 통계량 출력 (문자로 된 변수만. include = )
```


```python
# mpg 요약 통계량 출력 (문자, 숫자 변수 모두. include = )
```

cf) 함수(내장함수, 패키지 함수), 메서드, 어트리뷰트 <br>

- 내장 함수 : 가장 기본적인 함수로 파이썬에 내장. 함수명 및 괄호 입력해서 사용. ex) sum(var)

- 패키지 함수 : 패키지를 로드해야 사용. 패키지명 뒤에 점 찍고 함수명 및 괄호 입력해서 사용. <br>

  ex) pd.DataFrame({'x':[1, 2, 3]})

- 메서드 : '변수가 지니고 있는 함수'. 변수명 뒤에 점 찍고 메서드명 및 괄호 입력해서 사용. <br>

  ex) df.head()  <br> 

  = 변수의 자료구조에 따라 사용할 수 있는 메서드가 다르다.

- 어트리뷰트 : '변수가 지니고 있는 값'. 변수명 뒤에 점 찍고 어트리뷰트명 입력해서 사용. 괄호 X <br>

  ex) df.shape ; df.index ; df.columns  <br> 

  = 이 역시 변수의 자료구조에 따라 사용할 수 있는 어트리뷰트가 다르다.


## 05-2. 변수명 바꾸기(113-115쪽)

- 목적 : 변수명을 이해하기 쉬운 단어로 변경 -> 데이터를 수월하게 다룰 수 있음

- df.rename()



```python
# 데이터 프레임 생성

df_raw = pd.DataFrame({'var1':[1, 2, 1],
                       'var2':[2, 3, 2],})
df_raw
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>var1</th>
      <th>var2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



```python
df_new = df_raw.copy()
df_new
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>var1</th>
      <th>var2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 변수 var2를 v2로 수정해서 df_new에 담음
```

### [개인 실습] 혼자서 해보기(115쪽)

- mpg 데이터의 변수명은 긴 단어를 짧게 줄인 축약어로 되어 있다. cty는 도시 연비, hwy는 고속도로 연비를 의미한다. 변수명을 이해하기 쉬운 단어로 바꾸려 한다.


#### Q1 : mpg 데이터를 불러와 복사본을 만드세요.



```python
# 변수 mpg_ned에 저장
```

#### Q2 : 복사본 데이터를 이용해 cty는 city로, hwy는 highway로 수정하세요



```python
# 결과를 변수 mpg_ned에 저장
```

## 05-3. 파생변수 만들기(116-128쪽)



```python
# 데이터 프레임 생성

import pandas as pd

df = pd.DataFrame({'var1':[4, 3, 8], 
                   'var2':[2, 6, 1]})
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>var1</th>
      <th>var2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 변수 var1과 var2의 값을 더하여 var_sum 변수에 저장
```


```python
# 변수 var1과 var2의 평균을 구하여 var_mean 변수에 저장
```

### [Do it! 실습] mpg 통합 연비 변수 만들기 (117쪽)



```python
# mpg.csv 데이터 불러와서 변수 mpg에 담기
```


```python
# cty, hwy 두 변수를 더해 2로 나눠 도로 유형을 통합한 연비 변수를 만들어 total 변수에 저장

# mpg 앞부분 5행 출력
```


```python
# 통합 연비 변수의 평균 구하기: sum(), len() 함수 이용
```


```python
# 통합 연비 변수의 평균 구하기: mean() 함수 이용
```

### [Do it! 실습] 조건문을 활용해 파생변수 만들기 (118쪽)


#### 1. 기준값 정하기



```python
# mpg 통합 연비 변수 total의 요약통계량 출력

mpg['total'].describe()
```

<pre>
count    234.000000
mean      20.149573
std        5.050290
min       10.500000
25%       15.500000
50%       20.500000
75%       23.500000
max       39.500000
Name: total, dtype: float64
</pre>

```python
# 히스토그램으로 자동차들의 통합 연비 분포 파악하기: df.plot.hist() 이용
```

#### 2. 합격 판정 변수 만들기



```python
import numpy as np
```


```python
# total이 20 이상이면 pass, 그렇지 않으면 fail을 부여 -> test 변수에 저장

# mpg 앞부분 5개 출력
```

#### 3. 빈도표로 합격 판정 자동차 수 살펴보기



```python
# df.value_counts() 이용
```

#### 4. 막대 그래프로 빈도 표현하기



```python
# 연비 합격 빈도표를 변수 count_test에 할당
```


```python
# 연비 합격 빈도 막대 그래프 만들기
```


```python
# 축 이름 회전하기
```

### [Do it! 실습] 중첩 조건문 활용하기 (123쪽)


#### 1. 연비 등급 변수 만들기



```python
# total 기준으로 A, B, C 등급 부여해서 grade 변수에 저장: 30이상 A, 20이상 B, 20미만 C

# mpg 앞부분 5개 출력
```

#### 2. 빈도표와 막대 그래프로 연비 등급 살펴보기



```python
# 등급 빈도표 만들어 변수 count_grade에 저장
```


```python
# 등급 빈도 막대 그래프 만들기
```

##### 그래프에서 알파벳 순으로 막대 정렬하기



```python
# 등급 빈도표를 알파벳 순으로 정렬해서 변수 count_grade에 저장
```


```python
# 이렇게 저장한 count_grade를 막대 그래프로 표현
```

### 메서드 체이닝


### 필요한 만큼 범주 만들기

- A, B, C, D 등급 변수 만들기



```python
# np.where() 두 번 중첩 사용해서 그 결과를 변수 grade2에 저장
```


```python
# 등급 빈도표를 알파벳 순으로 정렬해서 변수 count_grade_2에 저장
```


```python
# 이렇게 저장한 count_grade_2를 막대 그래프로 표현
```

### [Do it! 실습] 목록에 해당하는 행으로 변수 만들기(128쪽)



```python
# 여러 조건 중 하나에 해당하면 특정 값을 부여해서 파생변수를 생성: "|"(or) 사용
# np.where()에 여러 조건 입력할 땐 각 조건을 괄호에 입력해야 함.
# category가 compact, subcompact, 2seater이면 -> small, 그렇지 않으면 large를 부여하여 파생변수 size를 생성

# 파생변수 빈도표 출력
```


```python
# 바로 위의 코드를 df.isin() 이용해서 간략화하기
```

## [분석 도전]

- midwest.csv는 미국 동북중부(East North Central States) 437개 지역의 인구통계 정보를 담고 있습니다. midwest.csv를 이용해 데이터 분석 문제를 해결해 보세요.

- midwest 데이터 출처: bit.ly/easypy_52


### 문제1

- midwest.csv를 불러와 midwest 변수에 넣고, 데이터의 특징을 파악하세요



```python
# 불러오기
```


```python
# 행과 열 개수
```


```python
# 요약통계량
```

### 문제2

- poptotal(전체 인구) 변수를 total로, popasian(아시아 인구) 변수를 asian으로 수정하세요.



```python
# midwest를 복사해서 midwest_new 변수에 저장하기
```


```python
# poptotal 변수는 total로 변경하고, popasian은 asian으로 변경하기
```

### 문제3

- total, asian 변수를 이용해 '전체 인구 대비 아시아 인구 백분율' 파생변수를 추가하고, 히스토그램을 만들어 분포를 살펴보세요.



```python
# 아시아 인구 백분율을 파생변수 asian_percent에 저장
```


```python
# 아시아 인구 백분율의 분포를 히스토그램으로 파악하기
```

### 문제4

- 아시아 인구 백분율 전체 평균을 구하고, 평균을 초과하면 'large', 그 외에는 'small'을 부여한 파생변수를 만들어 보세요.



```python
# 아시아 인구 백분율 전체 평균을 구하여  파생변수 average에 저장
```


```python
# large, small 값을 파생변수 group에 저장
```

### 문제 5:

- 'large'와 'small'에 해당하는 지역이 얼마나 많은지 빈도표와 빈도 막대 그래프를 만들어 확인해 보세요



```python
# 빈도표를 count_group 변수에 저장
```


```python
# 빈도 막대 그래프 작성
```

cf) 히스토그램과 막대그래프

1) 데이터 유형

- 히스토그램: 연속적인 수치 데이터를 다룹니다. 히스토그램은 변수의 분포를 보여주며, 일반적으로 수치적 데이터의 빈도수 또는 빈도 분포를 나타냅니다.

- 막대그래프: 범주형 데이터를 다룹니다. 각 범주는 서로 독립적이며, 각 범주의 빈도수나 양을 비교하는 데 사용됩니다.



2) 축

- 히스토그램: 수평축(x축)은 변수의 구간을 나타내며, 수직축(y축)은 빈도수 또는 밀도를 나타냅니다.

- 막대그래프: 수평축(x축)은 개별 범주를 나타내며, 수직축(y축)은 그 범주의 빈도수나 양을 나타냅니다.


# <span style="color:blue; font-weight:bold;">The End of Note</span>

