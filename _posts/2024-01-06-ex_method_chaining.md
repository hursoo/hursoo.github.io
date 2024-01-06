---
layout: single
title: "[23파이썬특강] 3강. 자유자재의 데이터 가공(메서드 체이닝의 쉬운 사례)"
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


# 1. 전체: 데이터 및 실행 코드



```python
import pandas as pd
import numpy as np

# 지정된 데이터셋 생성
df = pd.DataFrame({
    'student': ['철수', '영희', '철수', '영희', '철수', '영희', np.nan, '민수', '민수', '민수', '민지', '민지', '준호', '준호', '민지', '민수', '영희'],
    'english': [82.0, 90.0, 78.0, 92.0, 85.0, np.nan, 85.0, 88.0, 79.0, 81.0, np.nan, 91.0, 75.0, 90.0, 100.0, 99.0, 80.0],
    'math': [90.0, np.nan, 88.0, 92.0, np.nan, np.nan, 84.0, 82.0, 80.0, 78.0, 77.0, 79.0, 83.0, 85.0, 95.0, 95.0, 70.0],
    'history': [80.0, 85.0, 87.0, 89.0, 91.0, 93.0, 76.0, 78.0, 80.0, np.nan, 75.0, 77.0, 72.0, 74.0, 60.0, 90.0, 100.0],
    'term': ['2023-1', '2023-1', '2023-1', '2023-1', '2023-2', '2023-2', '2023-1', '2023-1', '2023-2', '2023-2', '2023-1', '2023-1', '2023-1', '2023-1', '2023-1', '2023-1', '2023-1']
})


# 판다스 메서드 체이닝을 사용한 데이터 처리
result = df.dropna(subset=['student', 'english', 'math', 'history']) \
           .query("term == '2023-1'") \
           .assign(average_score = lambda x: (x['english'] + x['math'] + x['history']) / 3) \
           .groupby('student') \
           .agg(mean_score = ('average_score', 'mean')) \
           .sort_values(by='mean_score', ascending=False) \
           .head(3)
         
result
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
      <th>mean_score</th>
    </tr>
    <tr>
      <th>student</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>민수</th>
      <td>88.666667</td>
    </tr>
    <tr>
      <th>영희</th>
      <td>87.166667</td>
    </tr>
    <tr>
      <th>철수</th>
      <td>84.166667</td>
    </tr>
  </tbody>
</table>
</div>


=================  
  

# 2. 메서드 체이닝 실습 데이터



```python
import pandas as pd
import numpy as np

# 지정된 데이터셋 생성
df = pd.DataFrame({
    'student': ['철수', '영희', '철수', '영희', '철수', '영희', np.nan, '민수', '민수', '민수', '민지', '민지', '준호', '준호', '민지', '민수', '영희'],
    'english': [82.0, 90.0, 78.0, 92.0, 85.0, np.nan, 85.0, 88.0, 79.0, 81.0, np.nan, 91.0, 75.0, 90.0, 100.0, 99.0, 80.0],
    'math': [90.0, np.nan, 88.0, 92.0, np.nan, np.nan, 84.0, 82.0, 80.0, 78.0, 77.0, 79.0, 83.0, 85.0, 95.0, 95.0, 70.0],
    'history': [80.0, 85.0, 87.0, 89.0, 91.0, 93.0, 76.0, 78.0, 80.0, np.nan, 75.0, 77.0, 72.0, 74.0, 60.0, 90.0, 100.0],
    'term': ['2023-1', '2023-1', '2023-1', '2023-1', '2023-2', '2023-2', '2023-1', '2023-1', '2023-2', '2023-2', '2023-1', '2023-1', '2023-1', '2023-1', '2023-1', '2023-1', '2023-1']
})

# 데이터셋 출력
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
      <th>student</th>
      <th>english</th>
      <th>math</th>
      <th>history</th>
      <th>term</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>철수</td>
      <td>82.0</td>
      <td>90.0</td>
      <td>80.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>영희</td>
      <td>90.0</td>
      <td>NaN</td>
      <td>85.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>철수</td>
      <td>78.0</td>
      <td>88.0</td>
      <td>87.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>영희</td>
      <td>92.0</td>
      <td>92.0</td>
      <td>89.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>철수</td>
      <td>85.0</td>
      <td>NaN</td>
      <td>91.0</td>
      <td>2023-2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>영희</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>93.0</td>
      <td>2023-2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>85.0</td>
      <td>84.0</td>
      <td>76.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>민수</td>
      <td>88.0</td>
      <td>82.0</td>
      <td>78.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>민수</td>
      <td>79.0</td>
      <td>80.0</td>
      <td>80.0</td>
      <td>2023-2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>민수</td>
      <td>81.0</td>
      <td>78.0</td>
      <td>NaN</td>
      <td>2023-2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>민지</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>75.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>민지</td>
      <td>91.0</td>
      <td>79.0</td>
      <td>77.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>준호</td>
      <td>75.0</td>
      <td>83.0</td>
      <td>72.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>준호</td>
      <td>90.0</td>
      <td>85.0</td>
      <td>74.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>민지</td>
      <td>100.0</td>
      <td>95.0</td>
      <td>60.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>민수</td>
      <td>99.0</td>
      <td>95.0</td>
      <td>90.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>영희</td>
      <td>80.0</td>
      <td>70.0</td>
      <td>100.0</td>
      <td>2023-1</td>
    </tr>
  </tbody>
</table>
</div>


# 3. 메스드 체이닝 코드



```python
# 판다스 메서드 체이닝을 사용한 데이터 처리
result = df.dropna(subset=['student', 'english', 'math', 'history']) \
           .query("term == '2023-1'") \
           .assign(average_score = lambda x: (x['english'] + x['math'] + x['history']) / 3) \
           .groupby('student') \
           .agg(mean_score = ('average_score', 'mean')) \
           .sort_values(by='mean_score', ascending=False) \
           .head(3)
         
result
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
      <th>mean_score</th>
    </tr>
    <tr>
      <th>student</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>민수</th>
      <td>88.666667</td>
    </tr>
    <tr>
      <th>영희</th>
      <td>87.166667</td>
    </tr>
    <tr>
      <th>철수</th>
      <td>84.166667</td>
    </tr>
  </tbody>
</table>
</div>


# 4. 코드 세부 검토


## 4.1. 결측치 제거



```python

result = df.dropna(subset=['student', 'english', 'math', 'history'])
result
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
      <th>student</th>
      <th>english</th>
      <th>math</th>
      <th>history</th>
      <th>term</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>철수</td>
      <td>82.0</td>
      <td>90.0</td>
      <td>80.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>철수</td>
      <td>78.0</td>
      <td>88.0</td>
      <td>87.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>영희</td>
      <td>92.0</td>
      <td>92.0</td>
      <td>89.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>민수</td>
      <td>88.0</td>
      <td>82.0</td>
      <td>78.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>민수</td>
      <td>79.0</td>
      <td>80.0</td>
      <td>80.0</td>
      <td>2023-2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>민지</td>
      <td>91.0</td>
      <td>79.0</td>
      <td>77.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>준호</td>
      <td>75.0</td>
      <td>83.0</td>
      <td>72.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>준호</td>
      <td>90.0</td>
      <td>85.0</td>
      <td>74.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>민지</td>
      <td>100.0</td>
      <td>95.0</td>
      <td>60.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>민수</td>
      <td>99.0</td>
      <td>95.0</td>
      <td>90.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>영희</td>
      <td>80.0</td>
      <td>70.0</td>
      <td>100.0</td>
      <td>2023-1</td>
    </tr>
  </tbody>
</table>
</div>


## 4.2. 2023-1 추출



```python
result = df.dropna(subset=['student', 'english', 'math', 'history']) \
           .query("term == '2023-1'")
result
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
      <th>student</th>
      <th>english</th>
      <th>math</th>
      <th>history</th>
      <th>term</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>철수</td>
      <td>82.0</td>
      <td>90.0</td>
      <td>80.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>철수</td>
      <td>78.0</td>
      <td>88.0</td>
      <td>87.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>영희</td>
      <td>92.0</td>
      <td>92.0</td>
      <td>89.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>민수</td>
      <td>88.0</td>
      <td>82.0</td>
      <td>78.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>민지</td>
      <td>91.0</td>
      <td>79.0</td>
      <td>77.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>준호</td>
      <td>75.0</td>
      <td>83.0</td>
      <td>72.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>준호</td>
      <td>90.0</td>
      <td>85.0</td>
      <td>74.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>민지</td>
      <td>100.0</td>
      <td>95.0</td>
      <td>60.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>민수</td>
      <td>99.0</td>
      <td>95.0</td>
      <td>90.0</td>
      <td>2023-1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>영희</td>
      <td>80.0</td>
      <td>70.0</td>
      <td>100.0</td>
      <td>2023-1</td>
    </tr>
  </tbody>
</table>
</div>


## 4.3. 파생변수로 성적 평균 추가



```python
result = df.dropna(subset=['student', 'english', 'math', 'history']) \
           .query("term == '2023-1'") \
           .assign(average_score = lambda x: (x['english'] + x['math'] + x['history']) / 3)
result
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
      <th>student</th>
      <th>english</th>
      <th>math</th>
      <th>history</th>
      <th>term</th>
      <th>average_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>철수</td>
      <td>82.0</td>
      <td>90.0</td>
      <td>80.0</td>
      <td>2023-1</td>
      <td>84.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>철수</td>
      <td>78.0</td>
      <td>88.0</td>
      <td>87.0</td>
      <td>2023-1</td>
      <td>84.333333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>영희</td>
      <td>92.0</td>
      <td>92.0</td>
      <td>89.0</td>
      <td>2023-1</td>
      <td>91.000000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>민수</td>
      <td>88.0</td>
      <td>82.0</td>
      <td>78.0</td>
      <td>2023-1</td>
      <td>82.666667</td>
    </tr>
    <tr>
      <th>11</th>
      <td>민지</td>
      <td>91.0</td>
      <td>79.0</td>
      <td>77.0</td>
      <td>2023-1</td>
      <td>82.333333</td>
    </tr>
    <tr>
      <th>12</th>
      <td>준호</td>
      <td>75.0</td>
      <td>83.0</td>
      <td>72.0</td>
      <td>2023-1</td>
      <td>76.666667</td>
    </tr>
    <tr>
      <th>13</th>
      <td>준호</td>
      <td>90.0</td>
      <td>85.0</td>
      <td>74.0</td>
      <td>2023-1</td>
      <td>83.000000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>민지</td>
      <td>100.0</td>
      <td>95.0</td>
      <td>60.0</td>
      <td>2023-1</td>
      <td>85.000000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>민수</td>
      <td>99.0</td>
      <td>95.0</td>
      <td>90.0</td>
      <td>2023-1</td>
      <td>94.666667</td>
    </tr>
    <tr>
      <th>16</th>
      <td>영희</td>
      <td>80.0</td>
      <td>70.0</td>
      <td>100.0</td>
      <td>2023-1</td>
      <td>83.333333</td>
    </tr>
  </tbody>
</table>
</div>


## 4.4. 학생별 그룹화



```python
result = df.dropna(subset=['student', 'english', 'math', 'history']) \
           .query("term == '2023-1'") \
           .assign(average_score = lambda x: (x['english'] + x['math'] + x['history']) / 3) \
           .groupby('student')
result.groups
```

<pre>
{'민수': [7, 15], '민지': [11, 14], '영희': [3, 16], '준호': [12, 13], '철수': [0, 2]}
</pre>

## 4.5. 학생별 과목 평균



```python
result = df.dropna(subset=['student', 'english', 'math', 'history']) \
           .query("term == '2023-1'") \
           .assign(average_score = lambda x: (x['english'] + x['math'] + x['history']) / 3) \
           .groupby('student') \
           .agg(mean_score = ('average_score', 'mean'))
result
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
      <th>mean_score</th>
    </tr>
    <tr>
      <th>student</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>민수</th>
      <td>88.666667</td>
    </tr>
    <tr>
      <th>민지</th>
      <td>83.666667</td>
    </tr>
    <tr>
      <th>영희</th>
      <td>87.166667</td>
    </tr>
    <tr>
      <th>준호</th>
      <td>79.833333</td>
    </tr>
    <tr>
      <th>철수</th>
      <td>84.166667</td>
    </tr>
  </tbody>
</table>
</div>


## 4.6. 평균점수를 정렬



```python
result = df.dropna(subset=['student', 'english', 'math', 'history']) \
           .query("term == '2023-1'") \
           .assign(average_score = lambda x: (x['english'] + x['math'] + x['history']) / 3) \
           .groupby('student') \
           .agg(mean_score = ('average_score', 'mean')) \
           .sort_values(by='mean_score', ascending=False)
result
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
      <th>mean_score</th>
    </tr>
    <tr>
      <th>student</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>민수</th>
      <td>88.666667</td>
    </tr>
    <tr>
      <th>영희</th>
      <td>87.166667</td>
    </tr>
    <tr>
      <th>철수</th>
      <td>84.166667</td>
    </tr>
    <tr>
      <th>민지</th>
      <td>83.666667</td>
    </tr>
    <tr>
      <th>준호</th>
      <td>79.833333</td>
    </tr>
  </tbody>
</table>
</div>


## 4.7. 상위점수 학생 3명 출력



```python
result = df.dropna(subset=['student', 'english', 'math', 'history']) \
           .query("term == '2023-1'") \
           .assign(average_score = lambda x: (x['english'] + x['math'] + x['history']) / 3) \
           .groupby('student') \
           .agg(mean_score = ('average_score', 'mean')) \
           .sort_values(by='mean_score', ascending=False) \
           .head(3)
         
result
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
      <th>mean_score</th>
    </tr>
    <tr>
      <th>student</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>민수</th>
      <td>88.666667</td>
    </tr>
    <tr>
      <th>영희</th>
      <td>87.166667</td>
    </tr>
    <tr>
      <th>철수</th>
      <td>84.166667</td>
    </tr>
  </tbody>
</table>
</div>

