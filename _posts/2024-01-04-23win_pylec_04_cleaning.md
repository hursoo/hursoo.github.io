---
layout: single
title: "[23파이썬특강] 4강. 데이터 정제와 그래프 시각화"
author_profile: false
toc : true
---

### 1. 개요
- 이곳 4강에서는 3강의 '데이터 가공'을 실전에서 활용하기 전에 익혀야 하는 두 가지 과정, 즉 데이터 정제와 그래프 시각화를 다룬다. 
- **데이터 정제**에는 빠진 데이터를 대상으로 하는 **결측치 정제**와, 이상한 데이터를 대상으로 하는 **이상치 정제**가 있다. 이상치에는 **극단치**도 포함되는데, 여기서는 '그래프 시각화'에도 나오는 상자 그림으로 극단치를 파악하는 방법을 알아 본다.
- **그래프 시각화**는 데이터를 그림으로 표현하는 작업으로, 이를 통해 데이터의 특징을 쉽게 이해할 수 있다. 대표적인 그래프로는 산점도, 막대 그래프, 선 그래프, 상자 그림 등이 있다. **seaborn** 패키지로 그래프를 그리는 데 필요한 명령어는 각 그래프별로 대체로 비슷하다. 중요한 것은 첫째, 각 그래프는 무엇을 표시할 때 유용한가를 파악하는 일이며, 둘째, 해당 함수의 파라미터에 넣은 데이터가 원자료 형태인지 요약 형태인지를 구분하는 일이다. 
- 실습 코드
	- [**2023win_python_lec_04_basic.ipynb**](https://github.com/hursoo/2023_winter_python-lecture/blob/main/excise_code/2023win_python_lec_04_basic.ipynb)
    - [**2023win_python_lec_04_full.ipynb**](https://github.com/hursoo/2023_winter_python-lecture/blob/main/excise_code/2023win_python_lec_04_full.ipynb)
   
     
- 실습 데이터
    - [**economic.csv**](https://github.com/youngwoos/Doit_Python)



### 2. 데이터 정제

#### 2.1. 결측치 정제하기
- 결측치 : 누락된 값, 비어 있는 값
- 결측치 있는 경우, 함수가 적용되지 않거나, 분석 결과가 왜곡되는 문제가 발생한다.
- 실제 데이터 분석시, 결측치 여부 확인해서 제거하는 **정제 과정**을 거친 다음에 분석해야 함

##### 2.1.1. 결측치 만들기
- Numpy 패키지의 **np.nan**을 입력 &rarr; NaN으로 표시

##### 2.1.2. 결측치 확인하기
- pd.isna()를 이용하면 결측치 포함 여부를 알 수 있다. 
- pd.isna().sum()으로 결측치 총 개수를 알 수 있다.

```python
pd.isna(df)
df.isna() # 이것도 바로 위 코드와 동일한 결과 산출

pd.isna(df).sum() 
df.isna().sum() # 이것도 바로 위 코드와 동일한 결과 산출

# 특정 열의 결측치 개수 파악할 경우
mpg[['drv', 'hwy']].isna().sum() # mpg[['drv', 'hwy']] 이것이 df에 해당한다고 생각하면 됨. 
```

##### 2.1.3. 결측치 제거하기
- df.dropna() 이용하면 결측치가 있는 "행"을 제거할 수 있다.
- 이 때 subset=[]의 대괄호 속에 결측치가 위치한 변수명을 입력한다.

```python
df_nomiss = df.dropna(subset = ['score']) # 변수가 하나일 때 subset = 'score' 도 동일한 결과 나옴
df_nomiss = df.dropna(subset = ['score', 'sex']) # 변수가 여러 개일 때
```


#### 2.2. 이상치 정제하기
- 이상치 : 정상 범위에서 크게 벗어난 값
- 이상치가 들어 있으면 분석 결과가 왜곡되므로 분석에 앞서 제거해야 함

##### 2.2.1. 이상치 확인하기
- df.value_counts() 이용해 빈도표를 만들면 됨

```python
df['sex'].value_counts().sort_index()
# df.value_counts()에 sort_index()를 적용하면 빈도 기준으로 내림차순 정렬하지 않고, 변수의 값 순서로 정렬
```

##### 2.2.2. 이상치를 결측 처리하기
- 확인한 이상치를 결측치로 변환
- np.where()를 이용해 이상치에 NaN을 부여

```python
# sex가 3일때, score가 5초과일 때 NaN 부여
import numpy as np
df = df.assign(sex = lambda x: np.where(x['sex'] == 3, np.nan, x['sex']), 
             score = lambda x: np.where(x['score'] > 5, np.nan, x['score']))
df
```

#### 2.3. 상자 그림으로 극단치 제거하기
- 극단치: 논리적으로 존재할 수 있지만 극단적으로 크거나 작은 값
    - 예) 몸무게 변수에 200kg 이상의 값이 있는 경우
- 극단치 제거 위해서는 먼저 어디까지를 정상 범위로 볼 것인가를 정해야 함
    - 논리적 판단에 의한 방법 : 성인 몸무게의 정상 범위를 40~150kg로 설정
    - 통계적 기준 이용 : 상하위 0.3% 또는 +-3 표준편차에 해당하는 값을 극단치로 간주
- **상자 그림으로 극단치 기준 정하기**
    - 상자 그림 : 데이터의 분포를 직사각형의 상자 모양으로 표현한 그래프 -> 데이터의 분포를 한눈에 알 수 있음

##### 2.3.1. 상자 그림 이해
- 상자 그림: 값을 크기 순으로 나열해 4등분 했을 때 위치하는 값인 '사분위수'를 이용해 만듦
- 상자 그림의 요소가 나타내는 값 &rarr; 교재 191쪽
- [quantile, quartile, percentile 개념 정리](https://blog.eunsukim.me/posts/understanding-quantile-quartile-and-percentile)
[**[중앙값(Median)과 상자그림(Box Plot) / 00:10:44]**(통계의 재발견, 2020-02-10)](https://www.youtube.com/watch?v=Wuk17zg-jt8)

##### 2.3.2. 극단치 기준값 구하기

```python
# 1사분위수, 3사분위수 구하기 : df.quantile() 이용
pct25 = mpg['hwy'].quantile(.25) # 하위 25%에 해당하는 1사분위수
pct75 = mpg['hwy'].quantile(.75) # 하위 75%에 해당하는 3사분위수

# IQR 구하기: IQR(inter quartile range, 사분위 범위) <- 1사분위수와 3사분위수 간의 거리
iqr = pct75 - pct25
iqr
```

```python
# 하한, 상한 구하기: 극단치의 경계값 (하한 - 1사분위수보다 'IQR의 1.5배'만큼 더 작은 값, 상한 - 3사분위수보다 더 큰 값)
print(pct25 - 1.5 * iqr) # 하한
print(pct75 + 1.5 * iqr) # 상한
```

<pre>
4.5
40.5
</pre>


##### 2.3.3. 극단치 제거

```python
# 극단치를 결측 처리하기 : np.where() 이용. 여러 조건 입력시 각 조건을 괄호로 감싸도록 주의
import numpy as np

# 변수를 특정해서(mpg['hwy']) 결측값으로 전환하는 방법
mpg['hwy'] = np.where((mpg['hwy'] < 4.5) | (mpg['hwy'] > 40.5), np.nan, mpg['hwy'])

# df 단위로 assign, lambda를 활용해서 결측값으로 전환하는 방법: 
## or 조건문은 다음과 같은 구조 속에 넣는다. np.where(()|(), , )
mpg = mpg.assign(hwy = np.where((x['hwy] < 4.5)|(x['hwy] > 40.5), np.nan, x['hwy']))

# 결측치 빈도 확인
mpg['hwy'].isna().sum() # isna()는 그 앞에 df뿐 아니라 df['var']도 올 수 있다.
```

```python
# 결측치 제거하고 분석하기 : 제거 -> drv(구동방식)에 따라 hwy 평균이 어떻게 다른지 알아보기
mpg.dropna(subset = ['hwy']) \
   .groupby('drv') \
   .agg(mean_hwy = ('hwy', 'mean'))
```


### 3. 그래프 시각화
- 그래프 : 데이터를 보기 쉽게 그림으로 표현한 것
- 데이터를 그래프로 표현하면 추세와 경향성이 드러나기 때문에 특징을 쉽게 이해할 수 있고, 그래프를 만드는 과정에서 새로운 패턴을 발견하기도 한다.
- 분석 결과를 발표할 때, 그래프를 활용하면 데이터의 특징을 잘 전달할 수 있다.
- seaborn은 그래프를 만들 때 많이 사용하는 패키지

#### 3.1. 산점도 - 변수 간 관계 표현하기
- 산점도(scatter plot) : 데이터를 x축과 y축에 점으로 표현한 그래프
- 나이와 소득처럼 **연속값으로 된 두 변수의 관계를 표현**할 때 사용
- sns.scatterplot() 이용
- data에 그래프를 그리는 데 사용할 데이터 프레임을 입력,
- x축과 y축에 사용할 변수를 따옴표(' ')를 이용해 문자 형태로 입력

```python
# x축은 displ, y축은 hwy를 나타낸 산점도 만들기
import seaborn as sns
sns.scatterplot(data = mpg, x = 'displ', y = 'hwy')
```
- 종류별로 표식 색깔 바꾸기: **hue** 이용

```python
# drv(구동 방식)별로 표식 색깔 다르게 표현
sns.scatterplot(data = mpg, x = 'displ', y = 'hwy', hue = 'drv')
```

#### 3.2. 막대 그래프 - 집단 간 차이 표현하기
- 막대그래프(bar chart) : 데이터의 크기를 막대의 길이로 표현한 그래프
- 성별 소득 차이처럼 집단 간 차이를 표현할 때 자주 사용
- 평균 막대 그래프 : 평균값의 크기를 막대 길이로 표현한 그래프
- seaborn 그래프를 그리기 위해서는, drv별 **그룹화 결과가** 인덱스 아닌 **변수 값으로** 나오게 해야 함: 다음과 같이 df.groupby()에 **as_index = False** 입력하면 됨

```python
# drv(구동 방식)별 hwy(고속도로 연비) 평균 
df_mpg = mpg.groupby('drv', as_index = False) \
            .agg(mean_hwy = ('hwy', 'mean'))
```

##### 3.2.1. 빈도 막대 그래프 만들기 1)
- sns.barplot() 이용
- data에 데이터 프레임을 지정, x축에 범주를 나타낸 변수, y축에 평균값을 나타낸 변수를 지정

```python
# drv별 hwy 평균을 나타낸 막대 그래프
sns.barplot(data = df_mpg, x = 'drv', y = 'mean_hwy');
```

##### 3.2.2. 빈도 막대 그래프 만들기 2)
- sns.countplot() 이용하면, df.groupby()와 df.agg() 이용하는 작업을 생략하고 곧바로 빈도 막대 그래프 만들 수 있다.

```python
# 빈도 막대 그래프 만들기
sns.countplot(data = mpg, x = 'drv');
```

#### 3.3. 선 그래프 - 시간에 따라 달라지는 데이터 표현하기

- 선 그래프 : 데이터를 선으로 표현한 그래프. 시간에 따라 달라지는 데이터를 표현할 때 자주 사용. 예) 환율, 주가지수 등 경제지표가 시간에 따라 변하는 양상
- 시계열 데이터 : 일별 환율처럼, 일정 시간 간격을 두고 나열된 데이터
- 시계열 그래프 : 시계열 데이터를 선으로 표현한 그래프

##### 3.3.1. 연도 변수 생성
- 먼저 변수 타입을 날짜 시간 타입(datetime64)으로 변경해야 함
- pd.to_datetime() 이용하면 변수 타입을 날짜 시간 타입으로 변경 가능

```python
# 날짜 시간 타입 변수 만들기
economics['date2'] = pd.to_datetime(economics['date'])
```

- 변수가 날짜 시간 타입이면 df.dt를 이용해 연, 월, 일을 추출 가능

```python
economics['date2'].dt.year   # 연 추출
economics['date2'].dt.month  # 월 추출
economics['date2'].dt.day    # 일 추출
```

- 연도 변수 추가

```python
economics['year'] = economics['date2'].dt.year
economics.head()
```

##### 3.3.2. x축에 연도 표시하기

```python
sns.lineplot(data = economics, x = 'year', y = 'unemploy', errorbar = None);
```

#### 4. 상자 그림 - 집단 간 분포 차이 표현하기
- 상자 그림(box plot): 데이터의 분포 또는 퍼져 있는 형태를 직사각형 상자 모양으로 표현한 그래프.
- 평균값을 볼 때보다 데이터의 특징을 더 자세히 이해할 수 있다.

##### 4.1. 상자 그림 만들기

```python
# mpg로 구동 방식별 고속도로 연비를 상자 그림으로 표현: 값 "자체" > 값 개수
mpg = pd. read_csv('mpg.csv')
sns.boxplot(data = mpg, x = 'drv', y = 'hwy');
```
##### 4.2. 상자 그림 이해 위한 작업

- 목표: 구동 방식별 고속도로 연비 구하기

##### 4.2.1. 먼저 '구동 방식' 값의 종류 파악

```
mpg.groupby('drv') \
   .agg(n = ('hwy', 'count')) \
   .sort_values(by = 'n', ascending = False)
```

##### 4.2.2. 이상치 있는 'f' 구동 방식의 분포 파악

```python
# f 방식 자동차의 hwy 연비"값" 분포도
mpg.query('drv == "f"') \
   .groupby('hwy') \
   .agg(n = ('hwy', 'count')) \
   .sort_index(ascending = False)
```

##### 4.2.3. 극단치 값 계산

```python
# 정상 범위 벗어난 값
pct25 = mpg_f['hwy'].quantile(.25)
pct75 = mpg_f['hwy'].quantile(.75)

iqr = pct75 - pct25

lowest = pct25 - iqr * 1.5  # 하한
highest = pct75 + iqr * 1.5 # 상한

print(lowest)
print(highest)
```

<pre>
21.5
33.5
</pre>

##### 4.2.4. 극단치 추출: 각 극단치의 개수 합계가 아니라 극단치 값 **종류**의 개수가 중요

```python
mpg_f.query('hwy > 33.5 | hwy < 21.5') \
     .groupby('hwy') \
     .agg(n = ('hwy', 'count')) \
     .sort_index(ascending = False)
```

