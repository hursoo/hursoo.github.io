---
layout: single
title: "[23파이썬특강] 3강. 자유자재의 데이터 가공"
author_profile: false
toc : true
---

### 1. 개요
- 이곳에서는 데이터를 자유자재로 다루기 위한 **가공** 방법을 익힌다. 데이터를 추출, 요약하고 여러 데이터를 합치는 방법 등이 그것이다.
- 실습 코드: 
	- [2023win_python_lec_03_basic.ipynb](???https://github.com/hursoo/2023_winter_python-lecture/blob/main/excise_code/2023win_python_lec_02_basic.ipynb)
    - [2023win_python_lec_03_full.ipynb](???https://github.com/hursoo/2023_winter_python-lecture/blob/main/excise_code/2023win_python_lec_02_full.ipynb)


### 2. 추출: query(), df[col_name]
#### 2.1. 조건 맞는 데이터(= 행) 추출
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

#### 2.2. 필요한 변수(= 열) 추출: 
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

#### 2.3. pandas 명령어 조합 (행과 열 추출)
- 
```python
exam.query('math >= 50')[['id', 'math']].head()
```

### 3. 정렬: sort_values()
- 순서대로 정렬
```python
exam.sort_values('math')                      # 오름차순 정렬
exam.sort_values('math', ascending = False)   # 내림차순 정렬
```
- 여러 변수 기준 정렬
```python
exam.sort_values(['nclass', 'math'], ascending = [True, False])
```

### 4. 파생변수 추가: assign()
- 한 개의 파생변수 추가
```python
exam.assign(total = exam['math'] + exam['english'] + exam['science'])
```
- 여러 파생변수 한꺼번에 추가
```python
exam.assign(total = exam['math'] + exam['english'] + exam['science'],
            mean = (exam['math'] + exam['english'] + exam['science']) / 3)
```
- assign()에 조건을 부여할 수 있는 np.where() 적용
```python
exam.assign(test = np.where(exam['science'] >= 60, 'pass', 'fall'))
```
- 추가한 변수를 pandas 코드에 바로 활용하기
```python
exam.assign(total = exam['math'] + exam['english'] + exam['science']) \
    .sort_values('total') \
    .head()
```

### 5. 집단별 요약: groupby(), agg()
- 
```python
exam.groupby(['nclass']) \
    .agg(mean_math = ('math', 'mean'))
```
- 각 집단별로 다시 집단 나누기
```python
exam.groupby(['manufacturer', 'drv']) \
    .agg(mean_cty = ('cty', 'mean'))
```

### 6. 데이터 합치기: merge(), concat()
- 가로로 합치기
```python
pd.merge(test1, test2, how = 'left', on = 'id')
```
- 세로로 합치기
```python
pd.concat([group_a, group_b])
```

