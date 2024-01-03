---
layout: single
title: "[23파이썬특강] 3강. 자유자재의 데이터 가공(코드 검색)"
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


# <span style="color:blue; font-weight:bold;">3강. 자유자재의 데이터 가공</span>

- 둘째마당 (06)

- pp.131-176 (46쪽)


## 06-1. 데이터 전처리 - 원하는 형태로 데이터 가공하기(132쪽)

- 데이터 전처리 : 분석에 적합하게 데이터를 가공하는 작업

- 추출, 종류별 분류, 데이터 합치기 등

- 판다스(pandas) : 전처리에 가장 많이 사용되는 패키지


주요 함수들

- query( ) : 행 추출

- df[ ] : 열(변수) 추출

- sort_value( ) : 정렬

- groupby( ) : 집단별로 나누기

- assign( ) : 변수 추가

- agg( ) : 통계치 구하기

- merge( ) : 데이터 합치기(열)

- concat( ) : 데이터 합치기(행)


## 06-2. 조건에 맞는 데이터만 추출하기(133-142쪽)


### [Do it! 실습] 조건에 맞는 데이터만 추출하기(133쪽)



```python
import pandas as pd
exam = pd.read_csv('exam.csv')
exam
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# exam에서 nclass가 1인 경우만 추출
exam.query('nclass == 1')   # '=='와 '='를 구별
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 2반의 경우만 추출
exam.query('nclass == 2')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 1반이 아닌 경우
exam.query('nclass != 1')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 3반이 아닌 경우
exam.query('nclass != 3')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 초과, 미만, 이상, 이하 조건 걸기(136쪽)



```python
# 수학 점수가 50점을 초과한 경우
exam.query('math > 50')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 수학 점수가 50점 미만인 경우
exam.query('math < 50')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 영어 점수가 50점 이상인 경우
exam.query('english >= 50')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 여러 조건을 충족하는 행 추출하기(138쪽)



```python
# 1반이면서 수학 점수가 50점 이상인 경우
exam.query('nclass == 1 & math >= 50')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 2반이면서 영어 점수가 80점 이상인 경우
exam.query('nclass == 2 & english >= 80')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 여러 조건 중 하나 이상 충족하는 행 추출하기(138쪽)



```python
# 수학 점수가 90점 이상이거나 영어 점수가 90점 이상인 경우
exam.query('math >= 90 | english >= 90')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 영어 점수가 90점 미만이거나 과학 점수가 50점 미만인 경우
exam.query('english < 90 | science < 50')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 목록에 해당하는 행 추출하기(139쪽)



```python
# 1, 3, 5반에 해당하면 추출
exam.query('nclass == 1 | nclass == 3 | nclass == 5')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 1, 3, 5반에 해당하면 추출 : in과 []를 사용
exam.query('nclass in [1, 3, 5]')
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 추출한 행으로 데이터 만들기(140쪽)

- 1반과 2반을 추출해 각각 새 데이터로 만든 다음,

- 두 반의 수학 점수 평균을 구하기



```python
# nclass가 1인 행 추출해 nclass1에 할당
nclass1 = exam.query('nclass == 1')

# nclass가 2인 행 추출해 nclass1에 할당
nclass2 = exam.query('nclass == 2')
```


```python
nclass1['math'].mean() # 1반 수학 점수 평균 구하기
```

<pre>
46.25
</pre>

```python
nclass2['math'].mean() # 2반 수학 점수 평균 구하기
```

<pre>
61.25
</pre>
### [Do it! 실습] 문자 변수를 이용해 조건에 맞는 행 추출하기(141쪽)

- 전체 조건을 감싸는 따옴표와, 추출할 문자를 감싸는 따옴표를 서로 다른 모양으로 입력해야 함.

- query(' ')처럼 작은 따옴표로 감쌌다면, 추출할 문자는 var == " "처럼 큰 따옴표로 감싸야 함.



```python
df = pd.DataFrame({'sex'     : ['F', 'M', 'F', 'M'],
                   'country' : ['Korea', 'China', 'Japan', 'USA']})
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
      <th>sex</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>F</td>
      <td>Korea</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M</td>
      <td>China</td>
    </tr>
    <tr>
      <th>2</th>
      <td>F</td>
      <td>Japan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M</td>
      <td>USA</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 전체 조건에 작은따옴표, 추출할 문자에 큰따옴표 사용: 여성 & 한국
df.query('sex == "F" & country == "Korea"')
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
      <th>sex</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>F</td>
      <td>Korea</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 반대로 전체 조건을 큰따옴표로 감쌌다면 추출할 문자는 작은따옴표로 감싸야 함: 남성 & 중국
df.query("sex == 'M' & country == 'China'")
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
      <th>sex</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>M</td>
      <td>China</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 전체 조건과 추출할 문자에 모두 작은따옴표 사용 => 에러
df.query('sex == 'F' & country == 'Korea'')
```

### [개인 실습] 혼자서 해보기(144쪽)

- mpg 데이터를 이용해 분석 문제를 해결해 보세요


#### Q1 : 자동차 배기량에 따른 고속도로 연비

- displ(배기량)이 4 이하인 자동차와 5 이상인 자동차 중 어떤 자동차의 hwy(고속도로 연비) 평균이 더 높은지 알아보세요



```python
# mpg.csv 파일을 불러와서 변수 mpg에 넣어라
mpg = pd.read_csv('mpg.csv')
mpg
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 11 columns</p>
</div>



```python
# 배기량(disp) 4 이하 자동차를 추출해서 변수 car_until4에 넣어라
car_until4 = mpg.query('displ <= 4')

# 배기량(disp) 5 이상 자동차를 추출해서 변수 car_from5에 넣어라
car_from5 = mpg.query('displ >= 5')

# 두 종류 자동차의 고속도로 연비(hwy) 평균을 각각 출력하고 어느 쪽이 높은지 비교하라.
print(car_until4['hwy'].mean())
print(car_from5['hwy'].mean())
```

<pre>
25.96319018404908
18.07894736842105
</pre>
#### Q2 : 자동차 제조 회사별 도시 연비

- 'audi'와 'toyota' 중 어느 manufacturer(자동차 제조 회사)의 cty(도시 연비) 평균이 더 높은지 알아보세요



```python
mpg[:3]
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 아우디와 토요타 회사를 각각 추출해서 audi, toyota라는 변수에 각각 할당하라.
audi = mpg.query('manufacturer == "audi"')
toyota = mpg.query('manufacturer == "toyota"')

# 두 회사 자동차의 도시 연비(cty) 평균을 각각 출력하고 어느 쪽이 높은지 비교하라.
print(audi['cty'].mean())
print(toyota['cty'].mean())
```

<pre>
17.61111111111111
18.529411764705884
</pre>
#### Q3 : 자동차별 고속도로 연비

- 'chevrolet', 'ford', 'honda' 자동차의 고속도로 연비 평균을 알아보려고 합니다. 세 회사의 데이터를 추출한 다음 hwy 전체 평균을 구해 보세요



```python
# 세 회사의 데이터를 각각 추출하여, chevrolet, ford, honda라는 변수에 각각 할당하라.
chevrolet = mpg.query("manufacturer == 'chevrolet'")
ford = mpg.query("manufacturer == 'ford'")
honda = mpg.query("manufacturer == 'honda'")

# 세 회사 자동차의 고속도로 연비(hwy) 평균을 각각 출력하라.
print(chevrolet['hwy'].mean())
print(ford['hwy'].mean())
print(honda['hwy'].mean())
```

<pre>
21.894736842105264
19.36
32.55555555555556
</pre>

```python
# 세 회사 고속도로 연비의 전체 평균을 구하라 (in, [ ] 사용). 변수는 three_manu에 할당.
three_manu = mpg.query("manufacturer in ['chevrolet', 'ford', 'honda']")
three_manu['hwy'].mean()
```

<pre>
22.50943396226415
</pre>
## 06-3. 필요한 변수만 추출하기(145-150쪽)


### [Do it! 실습] 변수 추출하기(145쪽)



```python
# exam에서 math 변수만 추출하기
exam['math']
```

<pre>
0     50
1     60
2     45
3     30
4     25
5     50
6     80
7     90
8     20
9     50
10    65
11    45
12    46
13    48
14    75
15    58
16    65
17    80
18    89
19    78
Name: math, dtype: int64
</pre>

```python
# exam에서 english 변수만 추출하기
exam['english']
```

<pre>
0     98
1     97
2     86
3     98
4     80
5     89
6     90
7     78
8     98
9     98
10    65
11    85
12    98
13    87
14    56
15    98
16    68
17    78
18    68
19    83
Name: english, dtype: int64
</pre>

```python
# 여러 변수 추출하기
exam[['nclass', 'math', 'english']]
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
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>50</td>
      <td>98</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>60</td>
      <td>97</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>45</td>
      <td>86</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>30</td>
      <td>98</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>25</td>
      <td>80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>50</td>
      <td>89</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>80</td>
      <td>90</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>90</td>
      <td>78</td>
    </tr>
    <tr>
      <th>8</th>
      <td>3</td>
      <td>20</td>
      <td>98</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3</td>
      <td>50</td>
      <td>98</td>
    </tr>
    <tr>
      <th>10</th>
      <td>3</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>3</td>
      <td>45</td>
      <td>85</td>
    </tr>
    <tr>
      <th>12</th>
      <td>4</td>
      <td>46</td>
      <td>98</td>
    </tr>
    <tr>
      <th>13</th>
      <td>4</td>
      <td>48</td>
      <td>87</td>
    </tr>
    <tr>
      <th>14</th>
      <td>4</td>
      <td>75</td>
      <td>56</td>
    </tr>
    <tr>
      <th>15</th>
      <td>4</td>
      <td>58</td>
      <td>98</td>
    </tr>
    <tr>
      <th>16</th>
      <td>5</td>
      <td>65</td>
      <td>68</td>
    </tr>
    <tr>
      <th>17</th>
      <td>5</td>
      <td>80</td>
      <td>78</td>
    </tr>
    <tr>
      <th>18</th>
      <td>5</td>
      <td>89</td>
      <td>68</td>
    </tr>
    <tr>
      <th>19</th>
      <td>5</td>
      <td>78</td>
      <td>83</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 변수 제거하기(147쪽)



```python
exam.drop(columns = 'math') # math 제거
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
      <th>id</th>
      <th>nclass</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 여러 변수 제거
exam.drop(columns = ['math', 'english'])
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
      <th>id</th>
      <th>nclass</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] pandas 함수 조합하기(148쪽)



```python
# query()와 [] 조합하기
# - 1반 학생의 영어 점수 추출

exam.query('nclass == 1')['english']
```

<pre>
0    98
1    97
2    86
3    98
Name: english, dtype: int64
</pre>

```python
# - 수학 점수가 50점 이상인 학생의 id와 math 변수 추출

exam.query('math >= 50')[['id', 'math']]
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
      <th>id</th>
      <th>math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>60</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>50</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>80</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>90</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>50</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>65</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>75</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>58</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>65</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>80</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>89</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>78</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 일부만 출력하기
# - math가 50 이상인 행만 추출한 다음, id, math 앞부분 5행까지 추출

exam.query('math >= 50')[['id', 'math']].head()
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
      <th>id</th>
      <th>math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>60</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>50</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>80</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



```python
# - math가 50 이상인 행만 추출한 다음 id, math 앞부분 10행까지 추출

exam.query('math >= 50')[['id', 'math']].head(10)
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
      <th>id</th>
      <th>math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>60</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>50</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>80</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>90</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>50</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>65</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>75</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>58</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>65</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 가독성 있게 코드 줄 바꾸기(150쪽)

- 1) 명령어 끝난 부분 뒤에 백슬래서(\)를 입력하고 Enter를 눌러 줄을 바꿈

- 2) Spacebar를 Tab을 이용해 간격을 띄우고 다음 명령어를 입력



```python
exam.query('math > 50') \
    [['id', 'math']] \
    .head(10)
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
      <th>id</th>
      <th>math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>60</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>80</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>90</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>65</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>75</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>58</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>65</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>80</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>89</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>78</td>
    </tr>
  </tbody>
</table>
</div>


### [개인 실습] 혼자서 해보기(150쪽)

- mpg 데이터를 이용해서 분석 문제를 해결하시오


#### Q1. category, cty 변수 추출

- mpg 데이터는 11개 변수로 구성. 이 중 category(자동차 종류), cty(도시 연비) 변수를 추출해서 새로운 데이터를 만드세요. 



```python
mpg = pd.read_csv('mpg.csv')
mpg.shape
```

<pre>
(234, 11)
</pre>

```python
# 'category', 'cty' 두 변수로 된 df를 mpg_new 변수에 할당
mpg_new = mpg[['category', 'cty']]
mpg_new
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
      <th>category</th>
      <th>cty</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>compact</td>
      <td>18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>compact</td>
      <td>21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>compact</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>compact</td>
      <td>21</td>
    </tr>
    <tr>
      <th>4</th>
      <td>compact</td>
      <td>16</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>midsize</td>
      <td>19</td>
    </tr>
    <tr>
      <th>230</th>
      <td>midsize</td>
      <td>21</td>
    </tr>
    <tr>
      <th>231</th>
      <td>midsize</td>
      <td>16</td>
    </tr>
    <tr>
      <th>232</th>
      <td>midsize</td>
      <td>18</td>
    </tr>
    <tr>
      <th>233</th>
      <td>midsize</td>
      <td>17</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 2 columns</p>
</div>


#### Q2 : 자동차 종류별 연비

- 앞에서 추출한 데이터를 이용해 category가 'suv'인 자동차와, 'compact'인 자동차 중 어떤 자동차의 cty 평균이 더 높은지 알아보시오.



```python
mpg_new.query('category == "suv"')['cty'].mean()
```

<pre>
13.5
</pre>

```python
mpg_new.query('category == "compact"')['cty'].mean()
```

<pre>
20.127659574468087
</pre>
## 06-4. 순서대로 정렬하기(151-153쪽)

- df.sort_values()


### [Do it! 실습] 오름차순으로 정렬하기(151쪽)



```python
# excel_exam.xlsx 데이터 불러와서 변수 exam에 넣어라
exam = pd.read_excel('excel_exam.xlsx')
exam
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# exam 데이터를 수학점수 낮은 사람부터 높은 사람 순으로 오름차순 정렬하기

exam.sort_values(['math'])
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 내림차순으로 정렬하기(152쪽)



```python
exam.sort_values(['math'], ascending = False) # math 내림차순 정렬
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 여러 정렬 기준 적용하기(152쪽)



```python
# 먼저 반을 기준으로 오름차순 정렬한 다음, 각 반에서 수학 점수를 기준으로 오름차순 정렬

exam.sort_values(['nclass', 'math'])
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 먼저 반을 기준으로 오름차순 정렬한 다음, 각 반에서 수학 점수를 기준으로 내림차순 정렬할 경우

exam.sort_values(['nclass', 'math'], ascending = [True, False])
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>


### [개인 실습] 혼자서 해보기(153쪽)

- mpg 데이터 이용하여 분석 문제 해결


#### Q1 : 'audi'가 생산한 자동차 중 높은 연비 모델

- 'audi'가 생산한 자동차 중에 어떤 자동차 모델의 hwy(고속도로 연비)가 높은지 알아보려 한다. hwy가 1~5위인 자동차의 데이터를 출력하라



```python
# mpg.csv 파일 불러와서 변수 mpg에 할당하라
mpg = pd.read_csv('mpg.csv')
mpg.head(3)
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
  </tbody>
</table>
</div>



```python
# audi 생산 자동차 중 hwy 상위 1-5위 자동차 데이터 출력
mpg.query('manufacturer == "audi"') \
    .sort_values(['hwy'], \
    ascending = False) \
    .head()
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>9</th>
      <td>audi</td>
      <td>a4 quattro</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>4</td>
      <td>20</td>
      <td>28</td>
      <td>p</td>
      <td>compact</td>
    </tr>
  </tbody>
</table>
</div>


## 06-5. 파생변수 추가하기(154-158쪽)

- 파생변수 : 변수를 조합하거나 함수를 이용해서 만든 "새 변수"

- df.assign( ) 이용


### [Do it! 실습] 파생변수 추가하기(154쪽)

- exam 세 과목 점수를 합한 총점 변수 추가하기



```python
# excel_exam.xlsx 데이터 불러와서 변수 exam에 넣어라
exam = pd.read_excel('excel_exam.xlsx')
exam
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# assign() 이용하여 수학, 영어, 과학 점수 합계를 total 변수에 저장 - 새로 만들 변수명에는 따옴표를 입력하지 않음 !!

exam.assign(total = exam['math'] + exam['english'] + exam['science'])
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
      <td>198</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
      <td>217</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
      <td>209</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
      <td>186</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
      <td>170</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
      <td>237</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
      <td>215</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
      <td>193</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
      <td>133</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
      <td>193</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>195</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
      <td>162</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
      <td>209</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
      <td>147</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
      <td>209</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
      <td>221</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
      <td>231</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
      <td>248</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
      <td>244</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
      <td>219</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 여러 파생변수 한 번에 추가: 세 과목 합계 점수는 total, 세 과목 평균 점수는 mean 변수에 할당

exam.assign(
    total = exam['math'] + exam['english'] + exam['science'], 
    mean = (exam['math'] + exam['english'] + exam['science']) / 3)
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
      <th>total</th>
      <th>mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
      <td>198</td>
      <td>66.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
      <td>217</td>
      <td>72.333333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
      <td>209</td>
      <td>69.666667</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
      <td>186</td>
      <td>62.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
      <td>170</td>
      <td>56.666667</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
      <td>237</td>
      <td>79.000000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
      <td>215</td>
      <td>71.666667</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
      <td>193</td>
      <td>64.333333</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
      <td>133</td>
      <td>44.333333</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
      <td>193</td>
      <td>64.333333</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>195</td>
      <td>65.000000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
      <td>162</td>
      <td>54.000000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
      <td>209</td>
      <td>69.666667</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
      <td>147</td>
      <td>49.000000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
      <td>209</td>
      <td>69.666667</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
      <td>221</td>
      <td>73.666667</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
      <td>231</td>
      <td>77.000000</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
      <td>248</td>
      <td>82.666667</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
      <td>244</td>
      <td>81.333333</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
      <td>219</td>
      <td>73.000000</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] df.assign( )에 np.where( ) 적용하기(156쪽)

- 조건에 따라 다른 값을 부여한 변수를 추가할 수 있음



```python
import numpy as np

# 과학 점수가 60점 이상일 때 pass, 60점 미만일 때 fall을 변수 test에 입력하라
exam.assign(test = np.where(exam['science'] >= 60, 'pass', 'fall'))
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
      <td>fall</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
      <td>fall</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
      <td>fall</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
      <td>fall</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
      <td>fall</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
      <td>fall</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
      <td>fall</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
      <td>fall</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
      <td>pass</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
      <td>fall</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 추가한 변수를 pandas 함수에 바로 활용하기(156쪽)



```python
# total 변수 추가하고 total의 값을 오름차순으로 정렬하라

exam.assign(total = exam['math'] + exam['english'] + exam['science']) \
    .sort_values(['total'])
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
      <td>133</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
      <td>147</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
      <td>162</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
      <td>170</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
      <td>186</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
      <td>193</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
      <td>193</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>195</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
      <td>198</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
      <td>209</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
      <td>209</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
      <td>209</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
      <td>215</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
      <td>217</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
      <td>219</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
      <td>221</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
      <td>231</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
      <td>237</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
      <td>244</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
      <td>248</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] lambda 이용해 데이터 프레임명 줄여 쓰기(157쪽)

- lambda x: 는 데이터 프레임명 자리에 x를 입력하겠다는 의미 -> 코드가 간결해짐



```python
# exam.csv 파일 불러와서 변수 long_name에 저장하라
long_name = pd.read_csv('exam.csv')
long_name
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 세 과목 합계를 new 변수에 할당: (종전대로) long_name라는 변수명을 직접 입력
long_name.assign(new = long_name['math'] + long_name['english'] + long_name['science'])
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
      <td>198</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
      <td>217</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
      <td>209</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
      <td>186</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
      <td>170</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
      <td>237</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
      <td>215</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
      <td>193</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
      <td>133</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
      <td>193</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>195</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
      <td>162</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
      <td>209</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
      <td>147</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
      <td>209</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
      <td>221</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
      <td>231</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
      <td>248</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
      <td>244</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
      <td>219</td>
    </tr>
  </tbody>
</table>
</div>



```python
# long_name 변수 대신 lambda와 x를 입력
long_name.assign(new = lambda x: x['math'] + x['english'] + x['science'])
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
      <td>198</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
      <td>217</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
      <td>209</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
      <td>186</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
      <td>170</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
      <td>237</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
      <td>215</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
      <td>193</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
      <td>133</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
      <td>193</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>195</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
      <td>162</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
      <td>209</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
      <td>147</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
      <td>209</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
      <td>221</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
      <td>231</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
      <td>248</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
      <td>244</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
      <td>219</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 앞에서 만든 변수를 활용해 다시 변수 만들기 (파생 변수를 이용해서 다시 파생 변수를 만들 때)

exam.assign(total = exam['math'] + exam['english'] + exam['science'], 
            mean =  lambda x: x['total'] / 3) # 코드를 읽기 불편 -> 두 행 모두 lambda 사용(다음 셀)
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
      <th>total</th>
      <th>mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
      <td>198</td>
      <td>66.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
      <td>217</td>
      <td>72.333333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
      <td>209</td>
      <td>69.666667</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
      <td>186</td>
      <td>62.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
      <td>170</td>
      <td>56.666667</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
      <td>237</td>
      <td>79.000000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
      <td>215</td>
      <td>71.666667</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
      <td>193</td>
      <td>64.333333</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
      <td>133</td>
      <td>44.333333</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
      <td>193</td>
      <td>64.333333</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>195</td>
      <td>65.000000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
      <td>162</td>
      <td>54.000000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
      <td>209</td>
      <td>69.666667</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
      <td>147</td>
      <td>49.000000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
      <td>209</td>
      <td>69.666667</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
      <td>221</td>
      <td>73.666667</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
      <td>231</td>
      <td>77.000000</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
      <td>248</td>
      <td>82.666667</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
      <td>244</td>
      <td>81.333333</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
      <td>219</td>
      <td>73.000000</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 좀 더 가독성이 높은 코드

exam.assign(total = lambda x: x['math'] + x['english'] + x['science'], 
            mean  = lambda x: x['total'] / 3)
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
      <th>total</th>
      <th>mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
      <td>198</td>
      <td>66.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
      <td>217</td>
      <td>72.333333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
      <td>209</td>
      <td>69.666667</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
      <td>186</td>
      <td>62.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
      <td>170</td>
      <td>56.666667</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
      <td>237</td>
      <td>79.000000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
      <td>215</td>
      <td>71.666667</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
      <td>193</td>
      <td>64.333333</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
      <td>133</td>
      <td>44.333333</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
      <td>193</td>
      <td>64.333333</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>195</td>
      <td>65.000000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
      <td>162</td>
      <td>54.000000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
      <td>209</td>
      <td>69.666667</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
      <td>147</td>
      <td>49.000000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
      <td>209</td>
      <td>69.666667</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
      <td>221</td>
      <td>73.666667</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
      <td>231</td>
      <td>77.000000</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
      <td>248</td>
      <td>82.666667</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
      <td>244</td>
      <td>81.333333</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
      <td>219</td>
      <td>73.000000</td>
    </tr>
  </tbody>
</table>
</div>



```python
exam.assign(total = exam['math'] + exam['english'] + exam['science'], 
            mean =  exam['total'] / 3)
```

### [개인 실습] 혼자서 해보기(158쪽)

- mpg 데이터는 연비를 나타내는 변수가 hwy(고속도로 연비), cty(도시 연비) 두 종류로 분리되어 있다. 두 변수를 각각 활용하는 대신 하나의 합산 연비 변수를 만들어 분석하려고 한다.


#### Q1 : mpg 데이터 복사본을 만들고, cty와 hwy를 더한 '합산 연비 변수'를 추가하시오

- 힌트: df.assign()을 적용한 결과를 =를 이용해 데이터 프레임에 할당하는 형태로 코드를 작성해야 함



```python
# mpg.csv 파일 불러와서 mpg에 할당하고 다시 이것을 복사해서 mpg_new 변수에 저장하라
mpg = pd.read_csv('mpg.csv')
mpg_new = mpg.copy()
mpg_new
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 11 columns</p>
</div>



```python
# 도시 연비와 고속도로 연비를 합한 값을 total 변수에 할당한 뒤 결과 df를 다시 mpg_new 변수에 담아라
mpg_new = mpg_new.assign(total = mpg_new['cty'] + mpg_new['hwy'])
mpg_new
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>47</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>50</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
      <td>51</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
      <td>51</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
      <td>42</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
      <td>47</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
      <td>50</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>42</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>44</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>43</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 12 columns</p>
</div>


#### Q2 : 앞에서 만든 '합산 연비 변수'를 2로 나눠 '평균 연비 변수'를 추가하세요



```python
# 평균 연비 변수를 mean에 할당하라
mpg_new = mpg_new.assign(mean = mpg_new['total'] / 2)
mpg_new
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
      <th>total</th>
      <th>average</th>
      <th>mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>47</td>
      <td>23.5</td>
      <td>23.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
      <td>50</td>
      <td>25.0</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
      <td>51</td>
      <td>25.5</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(av)</td>
      <td>f</td>
      <td>21</td>
      <td>30</td>
      <td>p</td>
      <td>compact</td>
      <td>51</td>
      <td>25.5</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>compact</td>
      <td>42</td>
      <td>21.0</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>229</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>19</td>
      <td>28</td>
      <td>p</td>
      <td>midsize</td>
      <td>47</td>
      <td>23.5</td>
      <td>23.5</td>
    </tr>
    <tr>
      <th>230</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>midsize</td>
      <td>50</td>
      <td>25.0</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>231</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>16</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>42</td>
      <td>21.0</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>232</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>2.8</td>
      <td>1999</td>
      <td>6</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>18</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>44</td>
      <td>22.0</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>233</th>
      <td>volkswagen</td>
      <td>passat</td>
      <td>3.6</td>
      <td>2008</td>
      <td>6</td>
      <td>auto(s6)</td>
      <td>f</td>
      <td>17</td>
      <td>26</td>
      <td>p</td>
      <td>midsize</td>
      <td>43</td>
      <td>21.5</td>
      <td>21.5</td>
    </tr>
  </tbody>
</table>
<p>234 rows × 14 columns</p>
</div>


#### Q3 : '평균 연비 변수'가 가장 높은 자동차 3종의 데이터를 출력하세요

- 힌트 : sort_values()와 head()를 조합하면 됩니다.



```python
mpg_new.sort_values('mean', ascending = False).head(3)
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
      <th>total</th>
      <th>average</th>
      <th>mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>221</th>
      <td>volkswagen</td>
      <td>new beetle</td>
      <td>1.9</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>35</td>
      <td>44</td>
      <td>d</td>
      <td>subcompact</td>
      <td>79</td>
      <td>39.5</td>
      <td>39.5</td>
    </tr>
    <tr>
      <th>212</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>1.9</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>33</td>
      <td>44</td>
      <td>d</td>
      <td>compact</td>
      <td>77</td>
      <td>38.5</td>
      <td>38.5</td>
    </tr>
    <tr>
      <th>222</th>
      <td>volkswagen</td>
      <td>new beetle</td>
      <td>1.9</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>29</td>
      <td>41</td>
      <td>d</td>
      <td>subcompact</td>
      <td>70</td>
      <td>35.0</td>
      <td>35.0</td>
    </tr>
  </tbody>
</table>
</div>


#### Q4 : 1~3번 문제를 해결할 수 있는 하나로 연결된 pandas 구문을 만들어 실행해 보세요. 데이터는 복사본 대신 mpg 원본을 이용하세요

- 힌트 : 앞에서 만든 코드를 연결하면 됩니다. 변수를 추가하는 작업을 하나의 assign()으로 구성하면 코드를 더 간결하게 만들 수 있습니다.



```python
mpg.assign(total = lambda x: x['cty'] + x['hwy'], \
           mean  = lambda x: x['total'] / 2) \
   .sort_values('mean', ascending = False) \
   .head(3)
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
      <th>total</th>
      <th>mean</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>221</th>
      <td>volkswagen</td>
      <td>new beetle</td>
      <td>1.9</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>35</td>
      <td>44</td>
      <td>d</td>
      <td>subcompact</td>
      <td>79</td>
      <td>39.5</td>
    </tr>
    <tr>
      <th>212</th>
      <td>volkswagen</td>
      <td>jetta</td>
      <td>1.9</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>33</td>
      <td>44</td>
      <td>d</td>
      <td>compact</td>
      <td>77</td>
      <td>38.5</td>
    </tr>
    <tr>
      <th>222</th>
      <td>volkswagen</td>
      <td>new beetle</td>
      <td>1.9</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l4)</td>
      <td>f</td>
      <td>29</td>
      <td>41</td>
      <td>d</td>
      <td>subcompact</td>
      <td>70</td>
      <td>35.0</td>
    </tr>
  </tbody>
</table>
</div>


## 06-6. 집단별로 요약하기(159-166쪽)

- '집단별 평균', '집단별 빈도'처럼 각 집단을 요약한 값을 구할 때 -> df.groupby()와 df.agg()를 사용

- 집단 간에 어떤 차이가 있는지 쉽게 파악 가능


### [Do it! 실습] 집단별로 요약하기(159쪽)


- 전체 요약 통계량 구하기 : df.agg() 사용

    - df.agg()에 mean_math = ('math', 'mean')처럼 요약값 할당한 변수명과 =를 입력한 다음, 

    - 값을 요약하는데 사용할 변수와 함수를 괄호 안에 나열




```python
# exam.csv 불러와서 exam 변수에 저장하라

import pandas as pd
exam = pd.read_csv('exam.csv')
exam.head(3)
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
  </tbody>
</table>
</div>



```python
# agg() 사용해서 수학 성적 평균을 구하고 그값을 변수 mean_math에 할당하라
exam.agg(mean_math = ('math', 'mean')) # 변수에 따옴표 넣지 않음. 함수명 뒤에 () 넣지 않음
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
      <th>math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mean_math</th>
      <td>57.45</td>
    </tr>
  </tbody>
</table>
</div>



```python
# mean() 이용하여 수학 성적 평균을 구하라
exam['math'].mean()  # 수학의 전체 평균. # agg()는 groupby()에 적용해 집단별 요약값 구할 때 사용
```

<pre>
57.45
</pre>
집단별 요약 통계량 구하기

- df.groupby()에 변수를 지정하면 변수의 범주별로 데이터를 분리

- 여기에 agg()를 적용하면, 집단별 요약 통계량이 나옴. 



```python
# 반별 수학 평균
exam.groupby('nclass') \
    .agg(mean_math = ('math', 'mean'))
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
      <th>mean_math</th>
    </tr>
    <tr>
      <th>nclass</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>46.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>61.25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>56.75</td>
    </tr>
    <tr>
      <th>5</th>
      <td>78.00</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 변수를 인덱스로 바꾸지 않기
exam.groupby('nclass', as_index = False) \
    .agg(mean_math = ('math', 'mean'))
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
      <th>nclass</th>
      <th>mean_math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>46.25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>61.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>45.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>56.75</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>78.00</td>
    </tr>
  </tbody>
</table>
</div>


여러 요약 통계량 한 번에 구하기

- df.agg()로 여러 요약 통계량을 한 번에 구할 수 있음. =:= df.assign()



```python
exam.groupby('nclass') \
    .agg(mean_math   = ('math', 'mean'), 
         sum_math    = ('math', 'sum'),
         median_math = ('math', 'median'),
         n           = ('nclass', 'count'))  # 빈도(학생 수)
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
      <th>mean_math</th>
      <th>sum_math</th>
      <th>median_math</th>
      <th>n</th>
    </tr>
    <tr>
      <th>nclass</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>46.25</td>
      <td>185</td>
      <td>47.5</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>61.25</td>
      <td>245</td>
      <td>65.0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45.00</td>
      <td>180</td>
      <td>47.5</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>56.75</td>
      <td>227</td>
      <td>53.0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>78.00</td>
      <td>312</td>
      <td>79.0</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 집단별로 다시 집단 나누기(163쪽)

- groupby()에 여러 변수를 지정하면, 집단을 나눈 다음 다시 하위 집단으로 나눌 수 있음.



```python
mpg.head(3)
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
  </tbody>
</table>
</div>



```python
# mpg 데이터로, 제조 회사별 집단을 나눈 다음 / 다시 구동 방식별로 나눠  -> 도시 연비 평균을 구하기
# dry의 4년 사륜구동, f는 전륜구동, r은 후륜구동을 의미

mpg = pd.read_csv('mpg.csv')
mpg.groupby(['manufacturer', 'drv']) \
   .agg(mean_cty = ('cty', 'mean'))
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
      <th></th>
      <th>mean_cty</th>
    </tr>
    <tr>
      <th>manufacturer</th>
      <th>drv</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">audi</th>
      <th>4</th>
      <td>16.818182</td>
    </tr>
    <tr>
      <th>f</th>
      <td>18.857143</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">chevrolet</th>
      <th>4</th>
      <td>12.500000</td>
    </tr>
    <tr>
      <th>f</th>
      <td>18.800000</td>
    </tr>
    <tr>
      <th>r</th>
      <td>14.100000</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">dodge</th>
      <th>4</th>
      <td>12.000000</td>
    </tr>
    <tr>
      <th>f</th>
      <td>15.818182</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">ford</th>
      <th>4</th>
      <td>13.307692</td>
    </tr>
    <tr>
      <th>r</th>
      <td>14.750000</td>
    </tr>
    <tr>
      <th>honda</th>
      <th>f</th>
      <td>24.444444</td>
    </tr>
    <tr>
      <th>hyundai</th>
      <th>f</th>
      <td>18.642857</td>
    </tr>
    <tr>
      <th>jeep</th>
      <th>4</th>
      <td>13.500000</td>
    </tr>
    <tr>
      <th>land rover</th>
      <th>4</th>
      <td>11.500000</td>
    </tr>
    <tr>
      <th>lincoln</th>
      <th>r</th>
      <td>11.333333</td>
    </tr>
    <tr>
      <th>mercury</th>
      <th>4</th>
      <td>13.250000</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">nissan</th>
      <th>4</th>
      <td>13.750000</td>
    </tr>
    <tr>
      <th>f</th>
      <td>20.000000</td>
    </tr>
    <tr>
      <th>pontiac</th>
      <th>f</th>
      <td>17.000000</td>
    </tr>
    <tr>
      <th>subaru</th>
      <th>4</th>
      <td>19.285714</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">toyota</th>
      <th>4</th>
      <td>14.933333</td>
    </tr>
    <tr>
      <th>f</th>
      <td>21.368421</td>
    </tr>
    <tr>
      <th>volkswagen</th>
      <th>f</th>
      <td>20.925926</td>
    </tr>
  </tbody>
</table>
</div>



```python
# audi 회사가 생산한 자동차의 구동방식(drv)별 자동차 대수
mpg.query('manufacturer == "audi"') \
   .groupby(['drv']) \
   .agg(n = ('drv', 'count'))
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
      <th>n</th>
    </tr>
    <tr>
      <th>drv</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>11</td>
    </tr>
    <tr>
      <th>f</th>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



```python
# chevrolet의 drv별 자동차 생산 대수

mpg.query('manufacturer == "chevrolet"') \
   .groupby(['drv']) \
   .agg(n = ('drv', 'count'))
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
      <th>n</th>
    </tr>
    <tr>
      <th>drv</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>4</td>
    </tr>
    <tr>
      <th>f</th>
      <td>5</td>
    </tr>
    <tr>
      <th>r</th>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] pandas 함수 조합하기(165쪽)


#### Q: suv 합산 연비 평균

- 제조 회사별로 'suv' 자동차의 도시 및 고속도로 합산 연비 평균을 구해 내림차순으로 정렬하고, 1~5위까지 출력하기


- 절차가 복잡해 보이는 분석도 pandas 함수를 조합하면 코드 몇 줄로 간단히 해결할 수 있다.

- 절차

    - 1. suv 추출 ----------------- query()

    - 2. 합산 연비 변수 만들기 ---- assign()

    - 3. 회사별로 분리 ------------ groupby()

    - 4. 합산 연비 평균 구하기 ---- agg()

    - 5. 내림차순 정렬 ------------ sort_values()

    - 6. 1~5위까지 출력 ----------- head()



```python
mpg.query('category == "suv"') \
   .assign(total = (mpg['cty'] + mpg['hwy']) / 2) \
   .groupby(['manufacturer']) \
   .agg(mean_tot = ('total', 'mean')) \
   .sort_values('mean_tot', ascending = False) \
   .head()
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
      <th>mean_tot</th>
    </tr>
    <tr>
      <th>manufacturer</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>subaru</th>
      <td>21.916667</td>
    </tr>
    <tr>
      <th>toyota</th>
      <td>16.312500</td>
    </tr>
    <tr>
      <th>nissan</th>
      <td>15.875000</td>
    </tr>
    <tr>
      <th>mercury</th>
      <td>15.625000</td>
    </tr>
    <tr>
      <th>jeep</th>
      <td>15.562500</td>
    </tr>
  </tbody>
</table>
</div>


### [개인 실습] 혼자서 해보기(166쪽)

- mpg 데이터를 이용해 분석 문제를 해결해 보세요


#### Q1: mpg 데이터의 category는 자동차를 특징에 따라 'suv', 'compact' 등 일곱 종류로 분류한 변수입니다. 어떤 차종의 도시 연비가 높은지 비교해 보려고 합니다. category별 cty 평균을 구해 보세요

- 힌트 : groupby()를 이용해 category별로 나눈 다음 agg()를 이용해 cty 평균을 구하면 됩니다.



```python
mpg.head(3)
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
  </tbody>
</table>
</div>



```python
mpg.groupby('category') \
   .agg(mean_cty = ('cty', 'mean'))
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
      <th>mean_cty</th>
    </tr>
    <tr>
      <th>category</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2seater</th>
      <td>15.400000</td>
    </tr>
    <tr>
      <th>compact</th>
      <td>20.127660</td>
    </tr>
    <tr>
      <th>midsize</th>
      <td>18.756098</td>
    </tr>
    <tr>
      <th>minivan</th>
      <td>15.818182</td>
    </tr>
    <tr>
      <th>pickup</th>
      <td>13.000000</td>
    </tr>
    <tr>
      <th>subcompact</th>
      <td>20.371429</td>
    </tr>
    <tr>
      <th>suv</th>
      <td>13.500000</td>
    </tr>
  </tbody>
</table>
</div>


#### Q2: 앞 문제 출력 결과에서, 어떤 차종의 도시 연비가 높은지 쉽게 알아볼 수 있도록, cty 평균이 높은 순으로 정렬해 출력하세요



```python
mpg.groupby('category') \
   .agg(mean_cty = ('cty', 'mean')) \
   .sort_values('mean_cty', ascending = False)
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
      <th>mean_cty</th>
    </tr>
    <tr>
      <th>category</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>subcompact</th>
      <td>20.371429</td>
    </tr>
    <tr>
      <th>compact</th>
      <td>20.127660</td>
    </tr>
    <tr>
      <th>midsize</th>
      <td>18.756098</td>
    </tr>
    <tr>
      <th>minivan</th>
      <td>15.818182</td>
    </tr>
    <tr>
      <th>2seater</th>
      <td>15.400000</td>
    </tr>
    <tr>
      <th>suv</th>
      <td>13.500000</td>
    </tr>
    <tr>
      <th>pickup</th>
      <td>13.000000</td>
    </tr>
  </tbody>
</table>
</div>


#### Q3: 어떤 회사 자동차의 hwy(고속도로 연비)가 가장 높은지 알아보려 한다. hwy 평균이 가장 높은 회사 세 곳을 출력하라 



```python
mpg.groupby('manufacturer') \
   .agg(mean_hwy = ('hwy', 'mean')) \
   .sort_values('mean_hwy', ascending = False) \
   .head(3)
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
      <th>mean_hwy</th>
    </tr>
    <tr>
      <th>manufacturer</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>honda</th>
      <td>32.555556</td>
    </tr>
    <tr>
      <th>volkswagen</th>
      <td>29.222222</td>
    </tr>
    <tr>
      <th>hyundai</th>
      <td>26.857143</td>
    </tr>
  </tbody>
</table>
</div>


#### Q4: 어떤 회사에서 'compact' 차종을 가장 많이 생산하는지 알아보려 한다. 회사별 'compact' 차종 수를 내림차순으로 정렬해 출력하라



```python
mpg.query('category == "compact"') \
   .groupby('manufacturer') \
   .agg(n = ('manufacturer', 'count')) \
   .sort_values('n', ascending = False)
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
      <th>n</th>
    </tr>
    <tr>
      <th>manufacturer</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>audi</th>
      <td>15</td>
    </tr>
    <tr>
      <th>volkswagen</th>
      <td>14</td>
    </tr>
    <tr>
      <th>toyota</th>
      <td>12</td>
    </tr>
    <tr>
      <th>subaru</th>
      <td>4</td>
    </tr>
    <tr>
      <th>nissan</th>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>


## 06-7. 데이터 합치기(167-172쪽)


### [Do it! 실습] 가로로 합치기(168쪽)



```python
# 중간고사 데이터 만들기
test1 = pd.DataFrame({'id'      : [1, 2, 3, 4, 5], 
                      'medterm' : [60, 80, 70, 90, 85]})

# 기말고사 데이터 만들기
test2 = pd.DataFrame({'id'      : [1, 2, 3, 4, 5],
                      'final'   : [70, 83, 65, 95, 80]})
```


```python
test1
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
      <th>id</th>
      <th>medterm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>



```python
test2
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
      <th>id</th>
      <th>final</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>



```python
# id 기준으로 합쳐서 total에 할당

total = pd.merge(test1, test2, how = 'left', on = 'id')
total
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
      <th>id</th>
      <th>medterm</th>
      <th>final</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>80</td>
      <td>83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>70</td>
      <td>65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>90</td>
      <td>95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>85</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 다른 데이터를 활용해 변수 추가하기 
## 'exam.csv' 불러와서 변수 exam에 저장하기

exam = pd.read_csv('exam.csv')
exam
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 새 데이터 프레임 생성해서 변수 name에 저장
name = pd.DataFrame({'nclass'  : [1, 2, 3, 4, 5],
                     'teacher' : ['kim', 'lee', 'park', 'choi', 'jung']})
name
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
      <th>nclass</th>
      <th>teacher</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>kim</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>lee</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>park</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>choi</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>jung</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 반별 담임교사 명단을 반영한 시험 데이터

exam_new = pd.merge(exam, name, how = 'left', on = 'nclass')
exam_new
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
      <th>id</th>
      <th>nclass</th>
      <th>math</th>
      <th>english</th>
      <th>science</th>
      <th>teacher</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>50</td>
      <td>98</td>
      <td>50</td>
      <td>kim</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>60</td>
      <td>97</td>
      <td>60</td>
      <td>kim</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>45</td>
      <td>86</td>
      <td>78</td>
      <td>kim</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>30</td>
      <td>98</td>
      <td>58</td>
      <td>kim</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2</td>
      <td>25</td>
      <td>80</td>
      <td>65</td>
      <td>lee</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>50</td>
      <td>89</td>
      <td>98</td>
      <td>lee</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2</td>
      <td>80</td>
      <td>90</td>
      <td>45</td>
      <td>lee</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2</td>
      <td>90</td>
      <td>78</td>
      <td>25</td>
      <td>lee</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>3</td>
      <td>20</td>
      <td>98</td>
      <td>15</td>
      <td>park</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>3</td>
      <td>50</td>
      <td>98</td>
      <td>45</td>
      <td>park</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>3</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>park</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>3</td>
      <td>45</td>
      <td>85</td>
      <td>32</td>
      <td>park</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>4</td>
      <td>46</td>
      <td>98</td>
      <td>65</td>
      <td>choi</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>4</td>
      <td>48</td>
      <td>87</td>
      <td>12</td>
      <td>choi</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>4</td>
      <td>75</td>
      <td>56</td>
      <td>78</td>
      <td>choi</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>4</td>
      <td>58</td>
      <td>98</td>
      <td>65</td>
      <td>choi</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>5</td>
      <td>65</td>
      <td>68</td>
      <td>98</td>
      <td>jung</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>5</td>
      <td>80</td>
      <td>78</td>
      <td>90</td>
      <td>jung</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>5</td>
      <td>89</td>
      <td>68</td>
      <td>87</td>
      <td>jung</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>5</td>
      <td>78</td>
      <td>83</td>
      <td>58</td>
      <td>jung</td>
    </tr>
  </tbody>
</table>
</div>


### [Do it! 실습] 세로로 합치기(170쪽)



```python
# 학생 1-5반 시험 데이터 만들기
group_a = pd.DataFrame({'id'   : [1, 2, 3, 4, 5], 
                        'test' : [60, 80, 70, 90, 85]})

# 학생 6-10번 시험 데이터 만들기
group_b = pd.DataFrame({'id'   : [6, 7, 8, 9, 10],
                        'test' : [70, 83, 65, 95, 80]})
```


```python
group_a
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
      <th>id</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>



```python
group_b
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
      <th>id</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7</td>
      <td>83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9</td>
      <td>95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>



```python
# group_a, group_b를 세로로 합해서 이를 group_all에 저장하라
group_all = pd.concat([group_a, group_b])
group_all
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
      <th>id</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>85</td>
    </tr>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7</td>
      <td>83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9</td>
      <td>95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 앞의 결과에서 인덱스 번호를 일련번호로 새로 지정하라
group_all = pd.concat([group_a, group_b], ignore_index = True)
group_all
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
      <th>id</th>
      <th>test</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>85</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>70</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>83</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>65</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>95</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>


### [개인 실습] 혼자서 해보기(173쪽)

- mpg 데이터를 이용해 분석 문제를 해결하시오



```python
mpg.head(3)
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
      <th>manufacturer</th>
      <th>model</th>
      <th>displ</th>
      <th>year</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drv</th>
      <th>cty</th>
      <th>hwy</th>
      <th>fl</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>auto(l5)</td>
      <td>f</td>
      <td>18</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>1</th>
      <td>audi</td>
      <td>a4</td>
      <td>1.8</td>
      <td>1999</td>
      <td>4</td>
      <td>manual(m5)</td>
      <td>f</td>
      <td>21</td>
      <td>29</td>
      <td>p</td>
      <td>compact</td>
    </tr>
    <tr>
      <th>2</th>
      <td>audi</td>
      <td>a4</td>
      <td>2.0</td>
      <td>2008</td>
      <td>4</td>
      <td>manual(m6)</td>
      <td>f</td>
      <td>20</td>
      <td>31</td>
      <td>p</td>
      <td>compact</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 새로운 데이터 프레임 생성: 자동차 연료별 가격

fuel = pd.DataFrame({'fl'       : ['c', 'd', 'e', 'p', 'r'],
                     'price_fl' : [2.35, 2.38, 2.11, 2.76, 2.22]})
fuel
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
      <th>fl</th>
      <th>price_fl</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c</td>
      <td>2.35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>d</td>
      <td>2.38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>e</td>
      <td>2.11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <th>4</th>
      <td>r</td>
      <td>2.22</td>
    </tr>
  </tbody>
</table>
</div>


#### Q1: fuel 데이터를 이용해 mpg 데이터에 price_fl(연료가격) 변수를 추가하라



```python
mpg = pd.merge(mpg, fuel, on = 'fl', how = 'left')
```

#### Q2: 연료 가격 변수가 잘 추가됐는지 확인하기 위해 model, fl, price_fl 변수를 추출해 앞부분 5행을 출력하라



```python
mpg = pd.merge(mpg, fuel, on = 'fl', how = 'left')
mpg[['model', 'fl', 'price_fl']].head()
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
      <th>model</th>
      <th>fl</th>
      <th>price_fl</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a4</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <th>1</th>
      <td>a4</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a4</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a4</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
    <tr>
      <th>4</th>
      <td>a4</td>
      <td>p</td>
      <td>2.76</td>
    </tr>
  </tbody>
</table>
</div>


### [분석 도전]

- 미국 동북중부 437개 지역 인구통계 정보를 담고 있는 midwest.csv를 사용해 데이터 분석 문제를 해결하라



```python
midwest = pd.read_csv('midwest.csv')
midwest
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
      <th>PID</th>
      <th>county</th>
      <th>state</th>
      <th>area</th>
      <th>poptotal</th>
      <th>popdensity</th>
      <th>popwhite</th>
      <th>popblack</th>
      <th>popamerindian</th>
      <th>popasian</th>
      <th>...</th>
      <th>percollege</th>
      <th>percprof</th>
      <th>poppovertyknown</th>
      <th>percpovertyknown</th>
      <th>percbelowpoverty</th>
      <th>percchildbelowpovert</th>
      <th>percadultpoverty</th>
      <th>percelderlypoverty</th>
      <th>inmetro</th>
      <th>category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>561</td>
      <td>ADAMS</td>
      <td>IL</td>
      <td>0.052</td>
      <td>66090</td>
      <td>1270.961540</td>
      <td>63917</td>
      <td>1702</td>
      <td>98</td>
      <td>249</td>
      <td>...</td>
      <td>19.631392</td>
      <td>4.355859</td>
      <td>63628</td>
      <td>96.274777</td>
      <td>13.151443</td>
      <td>18.011717</td>
      <td>11.009776</td>
      <td>12.443812</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>1</th>
      <td>562</td>
      <td>ALEXANDER</td>
      <td>IL</td>
      <td>0.014</td>
      <td>10626</td>
      <td>759.000000</td>
      <td>7054</td>
      <td>3496</td>
      <td>19</td>
      <td>48</td>
      <td>...</td>
      <td>11.243308</td>
      <td>2.870315</td>
      <td>10529</td>
      <td>99.087145</td>
      <td>32.244278</td>
      <td>45.826514</td>
      <td>27.385647</td>
      <td>25.228976</td>
      <td>0</td>
      <td>LHR</td>
    </tr>
    <tr>
      <th>2</th>
      <td>563</td>
      <td>BOND</td>
      <td>IL</td>
      <td>0.022</td>
      <td>14991</td>
      <td>681.409091</td>
      <td>14477</td>
      <td>429</td>
      <td>35</td>
      <td>16</td>
      <td>...</td>
      <td>17.033819</td>
      <td>4.488572</td>
      <td>14235</td>
      <td>94.956974</td>
      <td>12.068844</td>
      <td>14.036061</td>
      <td>10.852090</td>
      <td>12.697410</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>3</th>
      <td>564</td>
      <td>BOONE</td>
      <td>IL</td>
      <td>0.017</td>
      <td>30806</td>
      <td>1812.117650</td>
      <td>29344</td>
      <td>127</td>
      <td>46</td>
      <td>150</td>
      <td>...</td>
      <td>17.278954</td>
      <td>4.197800</td>
      <td>30337</td>
      <td>98.477569</td>
      <td>7.209019</td>
      <td>11.179536</td>
      <td>5.536013</td>
      <td>6.217047</td>
      <td>1</td>
      <td>ALU</td>
    </tr>
    <tr>
      <th>4</th>
      <td>565</td>
      <td>BROWN</td>
      <td>IL</td>
      <td>0.018</td>
      <td>5836</td>
      <td>324.222222</td>
      <td>5264</td>
      <td>547</td>
      <td>14</td>
      <td>5</td>
      <td>...</td>
      <td>14.475999</td>
      <td>3.367680</td>
      <td>4815</td>
      <td>82.505140</td>
      <td>13.520249</td>
      <td>13.022889</td>
      <td>11.143211</td>
      <td>19.200000</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>432</th>
      <td>3048</td>
      <td>WAUKESHA</td>
      <td>WI</td>
      <td>0.034</td>
      <td>304715</td>
      <td>8962.205880</td>
      <td>298313</td>
      <td>1096</td>
      <td>672</td>
      <td>2699</td>
      <td>...</td>
      <td>35.396784</td>
      <td>7.667090</td>
      <td>299802</td>
      <td>98.387674</td>
      <td>3.121060</td>
      <td>3.785820</td>
      <td>2.590061</td>
      <td>4.085479</td>
      <td>1</td>
      <td>HLU</td>
    </tr>
    <tr>
      <th>433</th>
      <td>3049</td>
      <td>WAUPACA</td>
      <td>WI</td>
      <td>0.045</td>
      <td>46104</td>
      <td>1024.533330</td>
      <td>45695</td>
      <td>22</td>
      <td>125</td>
      <td>92</td>
      <td>...</td>
      <td>16.549869</td>
      <td>3.138596</td>
      <td>44412</td>
      <td>96.330036</td>
      <td>8.488697</td>
      <td>10.071411</td>
      <td>6.953799</td>
      <td>10.338641</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>434</th>
      <td>3050</td>
      <td>WAUSHARA</td>
      <td>WI</td>
      <td>0.037</td>
      <td>19385</td>
      <td>523.918919</td>
      <td>19094</td>
      <td>29</td>
      <td>70</td>
      <td>43</td>
      <td>...</td>
      <td>15.064584</td>
      <td>2.620907</td>
      <td>19163</td>
      <td>98.854785</td>
      <td>13.786985</td>
      <td>20.050708</td>
      <td>11.695784</td>
      <td>11.804558</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
    <tr>
      <th>435</th>
      <td>3051</td>
      <td>WINNEBAGO</td>
      <td>WI</td>
      <td>0.035</td>
      <td>140320</td>
      <td>4009.142860</td>
      <td>136822</td>
      <td>697</td>
      <td>685</td>
      <td>1728</td>
      <td>...</td>
      <td>24.995504</td>
      <td>5.659847</td>
      <td>133950</td>
      <td>95.460376</td>
      <td>8.804031</td>
      <td>10.592031</td>
      <td>8.660587</td>
      <td>6.661094</td>
      <td>1</td>
      <td>HAU</td>
    </tr>
    <tr>
      <th>436</th>
      <td>3052</td>
      <td>WOOD</td>
      <td>WI</td>
      <td>0.048</td>
      <td>73605</td>
      <td>1533.437500</td>
      <td>72157</td>
      <td>90</td>
      <td>481</td>
      <td>722</td>
      <td>...</td>
      <td>21.666382</td>
      <td>4.583725</td>
      <td>72685</td>
      <td>98.750085</td>
      <td>8.525831</td>
      <td>11.162997</td>
      <td>7.375656</td>
      <td>7.882918</td>
      <td>0</td>
      <td>AAR</td>
    </tr>
  </tbody>
</table>
<p>437 rows × 28 columns</p>
</div>



```python
# 문제 1: popadults는 해당 지역의 성인 인구, poptotal은 전체 인구를 나태닌다. midwest 데이터에 '전체 인구 대비 미성년 인구 백분율' 변수를 추가하라

midwest_new = midwest.assign(ratio = 100 - (midwest['popadults'] / midwest['poptotal']) * 100)
midwest_new.head(3)
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
      <th>PID</th>
      <th>county</th>
      <th>state</th>
      <th>area</th>
      <th>poptotal</th>
      <th>popdensity</th>
      <th>popwhite</th>
      <th>popblack</th>
      <th>popamerindian</th>
      <th>popasian</th>
      <th>...</th>
      <th>percprof</th>
      <th>poppovertyknown</th>
      <th>percpovertyknown</th>
      <th>percbelowpoverty</th>
      <th>percchildbelowpovert</th>
      <th>percadultpoverty</th>
      <th>percelderlypoverty</th>
      <th>inmetro</th>
      <th>category</th>
      <th>ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>561</td>
      <td>ADAMS</td>
      <td>IL</td>
      <td>0.052</td>
      <td>66090</td>
      <td>1270.961540</td>
      <td>63917</td>
      <td>1702</td>
      <td>98</td>
      <td>249</td>
      <td>...</td>
      <td>4.355859</td>
      <td>63628</td>
      <td>96.274777</td>
      <td>13.151443</td>
      <td>18.011717</td>
      <td>11.009776</td>
      <td>12.443812</td>
      <td>0</td>
      <td>AAR</td>
      <td>34.486307</td>
    </tr>
    <tr>
      <th>1</th>
      <td>562</td>
      <td>ALEXANDER</td>
      <td>IL</td>
      <td>0.014</td>
      <td>10626</td>
      <td>759.000000</td>
      <td>7054</td>
      <td>3496</td>
      <td>19</td>
      <td>48</td>
      <td>...</td>
      <td>2.870315</td>
      <td>10529</td>
      <td>99.087145</td>
      <td>32.244278</td>
      <td>45.826514</td>
      <td>27.385647</td>
      <td>25.228976</td>
      <td>0</td>
      <td>LHR</td>
      <td>36.721250</td>
    </tr>
    <tr>
      <th>2</th>
      <td>563</td>
      <td>BOND</td>
      <td>IL</td>
      <td>0.022</td>
      <td>14991</td>
      <td>681.409091</td>
      <td>14477</td>
      <td>429</td>
      <td>35</td>
      <td>16</td>
      <td>...</td>
      <td>4.488572</td>
      <td>14235</td>
      <td>94.956974</td>
      <td>12.068844</td>
      <td>14.036061</td>
      <td>10.852090</td>
      <td>12.697410</td>
      <td>0</td>
      <td>AAR</td>
      <td>35.501301</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 29 columns</p>
</div>



```python
# 문제 2: 미성년 인구 백분율을 변수 ratio에 넣고, 이 백분율이 가장 높은 상위 5개 county(지역)의 미성년 인구 백분율을 출력하라

midwest_new.sort_values('ratio', ascending = False) \
        .head() \
        [['county', 'ratio']]
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
      <th>county</th>
      <th>ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>230</th>
      <td>ISABELLA</td>
      <td>51.501172</td>
    </tr>
    <tr>
      <th>404</th>
      <td>MENOMINEE</td>
      <td>50.591260</td>
    </tr>
    <tr>
      <th>281</th>
      <td>ATHENS</td>
      <td>49.320727</td>
    </tr>
    <tr>
      <th>247</th>
      <td>MECOSTA</td>
      <td>49.059183</td>
    </tr>
    <tr>
      <th>154</th>
      <td>MONROE</td>
      <td>47.358182</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 문제 3: 분류표 기준에 따라 미성년 비율 등급 변수를 추가하고, 각 등급에 몇 개의 지역이 있는지 알아보라

## 분류표 데이터 생성
class_table = pd.DataFrame({'분류' : ['large', 'middle', 'small'], 
                            '기준' : ['40% 이상', '30~40% 이상', '30% 이상']})
class_table
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
      <th>분류</th>
      <th>기준</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>large</td>
      <td>40% 이상</td>
    </tr>
    <tr>
      <th>1</th>
      <td>middle</td>
      <td>30~40% 이상</td>
    </tr>
    <tr>
      <th>2</th>
      <td>small</td>
      <td>30% 이상</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 미성년 비율 등급을 변수 grade에 추가

import numpy as np
midwest_new['grade'] = np.where(midwest_new['ratio'] >= 40, 'large',
                       np.where(midwest_new['ratio'] >= 30, 'middle', 'small'))
midwest_new.head(3)
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
      <th>PID</th>
      <th>county</th>
      <th>state</th>
      <th>area</th>
      <th>poptotal</th>
      <th>popdensity</th>
      <th>popwhite</th>
      <th>popblack</th>
      <th>popamerindian</th>
      <th>popasian</th>
      <th>...</th>
      <th>poppovertyknown</th>
      <th>percpovertyknown</th>
      <th>percbelowpoverty</th>
      <th>percchildbelowpovert</th>
      <th>percadultpoverty</th>
      <th>percelderlypoverty</th>
      <th>inmetro</th>
      <th>category</th>
      <th>ratio</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>561</td>
      <td>ADAMS</td>
      <td>IL</td>
      <td>0.052</td>
      <td>66090</td>
      <td>1270.961540</td>
      <td>63917</td>
      <td>1702</td>
      <td>98</td>
      <td>249</td>
      <td>...</td>
      <td>63628</td>
      <td>96.274777</td>
      <td>13.151443</td>
      <td>18.011717</td>
      <td>11.009776</td>
      <td>12.443812</td>
      <td>0</td>
      <td>AAR</td>
      <td>34.486307</td>
      <td>middle</td>
    </tr>
    <tr>
      <th>1</th>
      <td>562</td>
      <td>ALEXANDER</td>
      <td>IL</td>
      <td>0.014</td>
      <td>10626</td>
      <td>759.000000</td>
      <td>7054</td>
      <td>3496</td>
      <td>19</td>
      <td>48</td>
      <td>...</td>
      <td>10529</td>
      <td>99.087145</td>
      <td>32.244278</td>
      <td>45.826514</td>
      <td>27.385647</td>
      <td>25.228976</td>
      <td>0</td>
      <td>LHR</td>
      <td>36.721250</td>
      <td>middle</td>
    </tr>
    <tr>
      <th>2</th>
      <td>563</td>
      <td>BOND</td>
      <td>IL</td>
      <td>0.022</td>
      <td>14991</td>
      <td>681.409091</td>
      <td>14477</td>
      <td>429</td>
      <td>35</td>
      <td>16</td>
      <td>...</td>
      <td>14235</td>
      <td>94.956974</td>
      <td>12.068844</td>
      <td>14.036061</td>
      <td>10.852090</td>
      <td>12.697410</td>
      <td>0</td>
      <td>AAR</td>
      <td>35.501301</td>
      <td>middle</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 30 columns</p>
</div>



```python
# 각 등급별 지역 수 파악

midwest_new.groupby('grade') \
           .agg(n = ('grade', 'count'))
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
      <th>n</th>
    </tr>
    <tr>
      <th>grade</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>large</th>
      <td>32</td>
    </tr>
    <tr>
      <th>middle</th>
      <td>396</td>
    </tr>
    <tr>
      <th>small</th>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>



```python
# 문제 4: popasian은 해당 지역의 아시아인 인구를 나타낸다. 
# '전체 인구 대비 아시아인 인구 백분율' 변수를 추가하고, 
# 하위 10개 지역의 state(주), county(지역), 아시아인 인구 백분율을 출력하라
```


```python
# 아시아인 인구 백분율 변수는 ratio_asian으로 사용하라
midwest.assign(ratio_asian = midwest['popasian'] / midwest['poptotal'] * 100) \
       .sort_values('ratio_asian') \
       .head(10) \
       [['state', 'county', 'ratio_asian']]
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
      <th>state</th>
      <th>county</th>
      <th>ratio_asian</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>404</th>
      <td>WI</td>
      <td>MENOMINEE</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>105</th>
      <td>IN</td>
      <td>BENTON</td>
      <td>0.010592</td>
    </tr>
    <tr>
      <th>109</th>
      <td>IN</td>
      <td>CARROLL</td>
      <td>0.015950</td>
    </tr>
    <tr>
      <th>358</th>
      <td>OH</td>
      <td>VINTON</td>
      <td>0.027032</td>
    </tr>
    <tr>
      <th>390</th>
      <td>WI</td>
      <td>IRON</td>
      <td>0.032504</td>
    </tr>
    <tr>
      <th>85</th>
      <td>IL</td>
      <td>SCOTT</td>
      <td>0.053154</td>
    </tr>
    <tr>
      <th>112</th>
      <td>IN</td>
      <td>CLAY</td>
      <td>0.060716</td>
    </tr>
    <tr>
      <th>261</th>
      <td>MI</td>
      <td>OSCODA</td>
      <td>0.063759</td>
    </tr>
    <tr>
      <th>340</th>
      <td>OH</td>
      <td>PERRY</td>
      <td>0.066546</td>
    </tr>
    <tr>
      <th>73</th>
      <td>IL</td>
      <td>PIATT</td>
      <td>0.070749</td>
    </tr>
  </tbody>
</table>
</div>



```python
```


```python
```

# The End of Notebook

