---
layout: single
title: "[23파이썬특강] 3강. 자유자재의 데이터 가공"
author_profile: false
toc : true
---

### 1. 개요
- 이곳에서는 데이터를 자유자재로 다루기 위한 **가공** 방법을 익힌다. 데이터 가공이란 데이터를 추출, 요약하고 여러 데이터를 합치는 방법 등을 말한다.  
- 실습 코드: 
	- [2023win_python_lec_03_basic.ipynb](https://github.com/hursoo/2023_winter_python-lecture/blob/main/excise_code/2023win_python_lec_03_basic.ipynb)
    - [2023win_python_lec_03_full.ipynb](https://github.com/hursoo/2023_winter_python-lecture/blob/main/excise_code/2023win_python_lec_03_full.ipynb)
- 특히 다음 7개의 메서드는 데이터 가공에서 많이 사용되는 유용한 명령어이며, 본 특강의 3강 ~ 5강까지 분석의 중추를 이룬다.
- 메서드를 다음과 같이 분류하면 기억하기 쉽다.
    - |정리|&rarr; |정돈|&rarr; |정렬|
|:---:|:---:|:---:||:---:|:---:
|dropna()||groupby()||sort_values()|
|query()||agg()||head()|
|assign()|||||

- 세부 설명
    - **정리**: 데이터를 분석 필요에 맞게 줄이거나 늘리는 과정. 결측치 처리(dropna)와 행 선택(query) 작업은 줄이기, 파생 변수 생성(assign) 작업은 늘리기에 해당
    - **정돈**: '정리'된 데이터를 종류별로 요약하는 과정. 같은 종류끼리 그룹화(groupby)해서 집계(agg)하는 작업
    - **정렬**: '정리정돈'한 결과를 알기 쉽게 만드는 과정. 내림/오름차순 정렬(sort_values)하고, 일부만 표시(head, tail)하는 작업.

- 주의점
    - 분석 목적에 따라 7개의 메서드 중 일부는 생략될 수 있다. 
    - 각 메서드는 **입력 형식에 차이**가 있어서, **각 형식에 맞게 입력**해야 한다.

### 2. 간단한 예제에 의한 이해
- 주피터랩 파일(실습용): [ex_method_chaining.ipynb](https://github.com/hursoo/2023_winter_python-lecture/blob/main/excise_code/ex_method_chaining.ipynb)
- 주피터랩 파일(코드 검색용): [자유자재의 데이터 가공(메서드 체이닝)](http://hursoo.github.io/ex_method_chaining/)

### 3. 교재의 관련 내용
#### 3.1. 추출: query(), df[col_name]
##### 3.1.1. 조건 맞는 데이터(= 행) 추출
- 조건에 맞는 데이터 추출
```python
exam.query('english <= 80')
```
- 여러 조건 동시 충족
```python
exam.query('nclass == 1 & math >= 50')
```
- 여러 조건 중 하나 이상 충족
```python
exam.query('math >= 90 | english >= 90')
exam.query('nclass in [1, 3, 5]')
```

##### 3.1.2. 필요한 변수(= 열) 추출: 
- 변수 추출
```python
exam['math']                               # 한 변수 추출
exam[['nclass', 'math', 'english']]        # 여러 변수 추출
```
- 변수 제거
```python
exam.drop(columns = 'math')                # 한 변수 제거
exam.drop(columns = ['math', 'english'])   # 여러 변수 제거
```

##### 3.1.3. pandas 명령어 조합 (행과 열 추출)
- 
```python
exam.query('math >= 50')[['id', 'math']].head()
```

#### 3.2. 정렬: sort_values()
- 순서대로 정렬
```python
exam.sort_values('math')                      # 오름차순 정렬
exam.sort_values('math', ascending = False)   # 내림차순 정렬
```
- 여러 변수 기준 정렬
```python
exam.sort_values(['nclass', 'math'], ascending = [True, False])
```

#### 3.3. 파생변수 추가: assign()
- 한 개의 파생변수 추가
```python
exam.assign(total = exam['math'] + exam['english'] + exam['science'])
```
- 여러 파생변수 한꺼번에 추가
```python
exam.assign(total = exam['math'] + exam['english'] + exam['science'], \
            mean = (exam['math'] + exam['english'] + exam['science']) / 3)
```
- assign()에 조건을 부여할 수 있는 np.where() 적용
```python
exam.assign(test = np.where(exam['science'] >= 60, 'pass', 'fall'))
```
- 추가한 변수를 pandas 코드에 바로 활용하기
```python
exam.assign(total = lambda x: x['math'] + x['english'] + x['science']) \
    .sort_values('total') \
    .head()
```
    - lambda x: 람다 함수. 데이터 프레임 자리에 **x를 입력하겠다**는 의미 &larr 코드를 간결화

#### 3.4. 집단별 요약: groupby(), agg()
- 집단별 평균
```python
exam.groupby(['nclass']) \
    .agg(mean_math = ('math', 'mean'))
```
- 각 집단별로 다시 집단 나누기
```python
exam.groupby(['manufacturer', 'drv']) \
    .agg(mean_cty = ('cty', 'mean'))
```

#### 3.5. 데이터 합치기: merge(), concat()
- 가로로 합치기
```python
pd.merge(test1, test2, how = 'left', on = 'id')
```
- 세로로 합치기
```python
pd.concat([group_a, group_b])
```

### 4. 실습예제를 통한 유형별 적용(7개 메서드 중심)

- 
|구분|메서드|a|b|c|d|
|:---:|:---:|:---:|:---:|:---:|:---:|
||dropna()|||||
|정리|query()|ㅇ|ㅇ||ㅇ|
||assign()|||ㅇ|ㅇ|
|정돈|groupby()||||ㅇ|
||agg()|ㅇ|||ㅇ|
|정렬|sort_values()||ㅇ|ㅇ|ㅇ|
||head()||ㅇ|ㅇ|ㅇ|


a. 배기량(displ) **4이하** 자동차와 **5이상**인 자동차의 고속도로 연비(hwy) **평균** 비교 (&rarr; 교재 144, 150쪽)

```python
car_until4 = mpg.query("displ <= 4") \
                .agg(mean_hwy = ('hwy', 'mean'))
car_until4
car_from5 = mpg.query("displ > 5") \
               .agg(mean_hwy = ('hwy', 'mean'))
car_from5
```

b. 'audi'가 생산한 자동차 중에 hwy **상위 1~5위**인 자동차의 데이터 출력 (&rarr; 교재 153쪽)
```python
mpg.query("manufacturer == 'audi'") \
   .sort_values(by = 'hwy', ascending = False) \
   .head()
```
c. **합산** 연비 변수(hwy와 cty 포함)의 평균이 가장 높은 자동차 3종의 데이터를 출력하라 (&rarr; 교재 158쪽)
```python
mpg.assign(average = lambda x: (x['hwy'] + x['cty']) / 2) \
   .sort_values(by = 'average', ascending = False) \
   .head(3)
```
d. **제조 회사별**로 'suv' 자동차의 도시 및 고속도로 합산 연비 평균을 구해 내림차순으로 정렬하고, 1~5위까지 출력하기 (&rarr; 교재 166쪽)
```python
mpg.query("category == 'suv'") \
   .assign(total = lambda x: (x['cty'] + x['hwy']) / 2) \
   .groupby('manufacturer') \
   .agg(mean_total = ('total', 'mean')) \
   .sort_values(by = 'mean_total', ascending = False) \
   .head()
```
