---
layout: single
title: "[23파이썬특강] 1강. 개발환경과 기본개념(코드 검색)"
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


# <span style="color:blue; font-weight:bold;">1강. 데이터 분석 환경과 기본 개념</span>

- 첫째마당 (01-03)

- pp.014-073 (60쪽)


# 03. 데이터 분석에 필요한 연장 챙기기


## 03-1. 변하는 수, '변수' 이해하기(53-58쪽)

- 변수 : '변하는 수'. 다양한 값을 지닌 하나의 속성 -> 데이터는 변수들의 덩어리.

- 변수는 데이터 분석의 '대상'이다. 

- 데이터 분석 : 변수 간의 관계를 파악하는 작업.


### [Do it! 실습] 변수 만들기(54쪽)



```python
# 변수 a에 숫자 1을 할당
a = 1
a
```

<pre>
1
</pre>

```python
# 변수 b에 숫자 2를 할당
b = 2
b
```

<pre>
2
</pre>

```python
# 변수 c에 숫자 3을 할당
c = 3
c
```

<pre>
3
</pre>

```python
# # 변수 d에 숫자 3.5를 할당
d = 3.5
d
```

<pre>
3.5
</pre>

```python
# 변수 a와 b를 더하라
a + b
```

<pre>
3
</pre>

```python
# 변수 a와 b와 c를 더하라
a + b + c
```

<pre>
6
</pre>

```python
# 4를 변수 b의 값으로 나누어라
4 / b
```

<pre>
2.0
</pre>

```python
# 5에 변수 b값을 곱해라
5 * b
```

<pre>
10
</pre>

```python
# 변수명 정하기 규칙(55쪽) - 문자로 시작, 영문 권장, 소문자
```

### [Do it! 실습] 여러 값으로 구성된 변수 만들기(56쪽)



```python
# [1, 2, 3]을 변수 var1에 할당하라
var1 = [1, 2, 3]
var1
```

<pre>
[1, 2, 3]
</pre>

```python
# [4, 5, 6]을 변수 var2에 할당하라
var2 = [4, 5, 6]
var2
```

<pre>
[4, 5, 6]
</pre>

```python
# 두 변수 var1과 var2를 더하라
var1 + var2
```

<pre>
[1, 2, 3, 4, 5, 6]
</pre>
### [Do it! 실습] 문자로 된 변수 만들기(57쪽)



```python
# 문자 x를 변수 str1에 할당하라
str1 = 'x'
str1
```

<pre>
'x'
</pre>

```python
# text라는 단어를 변수 str2에 넣어라
str2 = 'text'
str2
```

<pre>
'text'
</pre>

```python
# Hello World!라는 구문을 변수 str3에 넣어라
str3 = 'Hello World!'
str3
```

<pre>
'Hello World!'
</pre>

```python
# ['a', 'b', 'c']를 변수 str4에 할당하라
str4 = ['a', 'b', 'c']
str4
```

<pre>
['a', 'b', 'c']
</pre>

```python
# ['Hello', 'World', 'is', 'good']를 변수 str5에 할당하라
str5 = ['Hello', 'World', 'is', 'good']
str5
```

<pre>
['Hello', 'World', 'is', 'good']
</pre>

```python
# 변수 str2와 str3을 더하라.
str2 + str3
```

<pre>
'textHello World!'
</pre>

```python
# 변수 str2와 str3을 더하되 그 사이에 공백 한 칸을 삽입하라.
str2 + " " + str3
```

<pre>
'text Hello World!'
</pre>

```python
# 문자로 된 변수로는 연산할 수 없다.
str1 + 2
```

## 03-2. 마술 상자 같은 '함수' 이해하기(59-61쪽)

- 데이터 분석은 '함수를 이용해서 변수를 조작하는 일'이다.

- 함수 : 입력값에 특정 기능을 수행하여 처음과 다른 값을 산출


### [Do it! 실습] 함수 이용하기(60쪽)

- 함수 : 함수 이름 + 괄호

- 함수 =:= 특정 기능을 하는 상자



```python
# 변수 만들기: [1, 2, 3]을 변수 x에 할당하라.
x = [1, 2, 3]
x
```

<pre>
[1, 2, 3]
</pre>

```python
# 함수 적용하기: x의 각 값을 모두 합하라
sum(x)
```

<pre>
6
</pre>

```python
# 최대값: x의 최대값 구하기
max(x)
```

<pre>
3
</pre>

```python
# 최소값: x의 최소값 구하기
min(x)
```

<pre>
1
</pre>

```python
# 함수의 결과물로 새 변수 만들기: x 각 값을 합한 뒤 이 값을 변수 x_sum에 넣어라
x_sum = sum(x)
x_sum
```

<pre>
6
</pre>

```python
# 함수의 결과물로 새 변수 만들기: x의 최대값을 변수 x_max에 넣어라
x_max = max(x)
x_max
```

<pre>
3
</pre>
## 03-3. 함수 꾸러미, '패키지' 이해하기(62-73쪽)



- 패키지 =:= 함수가 여러 개 들어 있는 꾸러미


### [Do it! 실습] 패키지 활용하기(63쪽)

- 패키지 사용하려면, 패키지를 <span style="color:red">설치</span>한 다음 로드해야 함.

- 패키지 설치는 한 번만 하면 됨. But <span style="color:red">로드는 JupyterLab 새로 시작할 때마다</span> 반복해야 함.

- 아나콘다에는 주요 패키지가 대부분 들어 있다.


#### 패키지 함수 사용하기

- seaborn 패키지의 countplot() 함수 -> 빈도 막대 그래프 작성



```python
import seaborn  # 패키지 로드
```


```python
# ['a', 'a', 'b', 'c']를 변수 var에 넣어라
var = ['a', 'a', 'b', 'c']
var
```

<pre>
['a', 'a', 'b', 'c']
</pre>

```python
# var 값으로 x축을 구성해 빈도 막대 그래프를 출력하라: seaborn 패키지 함수 countplot() 사용
seaborn.countplot(x = var)
```

<pre>
<Axes: ylabel='count'>
</pre>
<img src="data:image/png;base64,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"/>

#### 설치하거나 로드하지 않고 사용하는 내장함수

- sum() max() min() 등


#### 패키지 약어 활용하기



```python
# seaborn 패키지를 불러와서 sns라는 약어를 부여하라
import seaborn as sns
```


```python
# var 값으로 x축을 구성해 빈도 막대 그래프를 출력하라
sns.countplot(x = var)
```

<pre>
<Axes: ylabel='count'>
</pre>
<img src="data:image/png;base64,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"/>

### [Do it! 실습] seaborn의 titanic 데이터로 그래프 만들기(66쪽)

- seabron 패키지의 dataload_dataset()를 이용하면 seaborn 패키지에 들어 있는 데이터를 불러올 수 있음.

- titanic 데이터



```python
df = sns.load_dataset('titanic')
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
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>embarked</th>
      <th>class</th>
      <th>who</th>
      <th>adult_male</th>
      <th>deck</th>
      <th>embark_town</th>
      <th>alive</th>
      <th>alone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>C</td>
      <td>Cherbourg</td>
      <td>yes</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>Third</td>
      <td>woman</td>
      <td>False</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>C</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>True</td>
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
    </tr>
    <tr>
      <th>886</th>
      <td>0</td>
      <td>2</td>
      <td>male</td>
      <td>27.0</td>
      <td>0</td>
      <td>0</td>
      <td>13.0000</td>
      <td>S</td>
      <td>Second</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>True</td>
    </tr>
    <tr>
      <th>887</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>19.0</td>
      <td>0</td>
      <td>0</td>
      <td>30.0000</td>
      <td>S</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>B</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>888</th>
      <td>0</td>
      <td>3</td>
      <td>female</td>
      <td>NaN</td>
      <td>1</td>
      <td>2</td>
      <td>23.4500</td>
      <td>S</td>
      <td>Third</td>
      <td>woman</td>
      <td>False</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>False</td>
    </tr>
    <tr>
      <th>889</th>
      <td>1</td>
      <td>1</td>
      <td>male</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>30.0000</td>
      <td>C</td>
      <td>First</td>
      <td>man</td>
      <td>True</td>
      <td>C</td>
      <td>Cherbourg</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>890</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>32.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.7500</td>
      <td>Q</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Queenstown</td>
      <td>no</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 15 columns</p>
</div>


#### 함수의 다양한 기능 이용하기(66쪽)

- 파라미터(매개변수) : 함수의 옵션을 설정하는 명령어.<br> 

  ex) countplot()에 입력한 'x'



```python
# countplot()의 data 파라미터에 df를 지정하고, 
# x 파라미터에 sex를 지정해서 
#'성별 빈도 막대 그래프'를 만들어라

sns.countplot(data = df, x = 'sex')
```

<pre>
<Axes: xlabel='sex', ylabel='count'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAjsAAAGyCAYAAAACgQXWAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8pXeV/AAAACXBIWXMAAA9hAAAPYQGoP6dpAAAnsklEQVR4nO3dfXRU9YH/8c+QkCFAMpIAM0QiDWu0aKJi9LAE2lAIyaYLtqVrLLCIK+1Co6HhQR5kQWA1KXAEVNZUspTwcGjq0bLbHhUIVlIhRUKUU56WWowlnGaM2DgTIE4gufvH/ri/Dg8KIWEmX96vc+45zvd+5+Z79Yx5nzt3Jg7LsiwBAAAYqkuoFwAAANCRiB0AAGA0YgcAABiN2AEAAEYjdgAAgNGIHQAAYDRiBwAAGI3YAQAARiN2AACA0SJDvYBw0Nraqr/85S+KiYmRw+EI9XIAAMBVsCxLjY2NSkhIUJcuX3L9xgqxkydPWhMnTrTi4uKs6Oho695777X2799v729tbbWeeeYZq1+/fla3bt2sjIwM69ChQ0HH+OKLL6wnn3zSio+Pt7p3726NHTvWqq2tveo11NbWWpLY2NjY2NjYOuH2Vb/zQ3plp6GhQcOGDdO3vvUtvfXWW+rbt6+OHz+uW265xZ6zfPlyrVy5UqWlpbrjjjv07LPPavTo0Tp27JhiYmIkSQUFBfrNb36jsrIyxcfHa9asWRozZoyqq6sVERHxleu4cJza2lrFxsZ2yLkCAID25ff7lZiYaP8evxKHZYXuD4HOmzdPe/bs0bvvvnvZ/ZZlKSEhQQUFBZo7d64kKRAIyO12a9myZZo6dap8Pp/69OmjTZs26ZFHHpEk/eUvf1FiYqLefPNNZWdnf+U6/H6/XC6XfD4fsQMAQCdxtb+/Q3qD8q9//Ws98MADevjhh9W3b18NHjxYJSUl9v6amhp5vV5lZWXZY06nUxkZGaqsrJQkVVdX69y5c0FzEhISlJKSYs+5WCAQkN/vD9oAAICZQho7H330kYqLi5WcnKzt27dr2rRpmj59ujZu3ChJ8nq9kiS32x30PLfbbe/zer2KiopSr169rjjnYkVFRXK5XPaWmJjY3qcGAADCREhjp7W1Vffff78KCws1ePBgTZ06VT/60Y9UXFwcNO/iT0hZlvWVn5r6sjnz58+Xz+ezt9ra2us7EQAAELZCGjv9+vXTXXfdFTQ2aNAgnThxQpLk8Xgk6ZIrNPX19fbVHo/Ho+bmZjU0NFxxzsWcTqdiY2ODNgAAYKaQxs6wYcN07NixoLE//vGPGjBggCQpKSlJHo9H5eXl9v7m5mZVVFQoPT1dkpSWlqauXbsGzamrq9OhQ4fsOQAA4OYV0o+ez5gxQ+np6SosLFRubq727duntWvXau3atZL+7+2rgoICFRYWKjk5WcnJySosLFT37t01YcIESZLL5dKUKVM0a9YsxcfHKy4uTrNnz1ZqaqoyMzNDeXoAACAMhDR2HnzwQW3dulXz58/X0qVLlZSUpNWrV2vixIn2nDlz5qipqUl5eXlqaGjQkCFDtGPHjqDP1K9atUqRkZHKzc1VU1OTRo0apdLS0qv6jh0AAGC2kH7PTrjge3YAAOh8OsX37AAAAHQ0YgcAABiN2AEAAEYjdgAAgNGIHQAAYDRiBwAAGI3YAQAARgvplwrebNKe2hjqJQBhp3rFo6FeAgDDcWUHAAAYjdgBAABGI3YAAIDRiB0AAGA0YgcAABiN2AEAAEYjdgAAgNGIHQAAYDRiBwAAGI3YAQAARiN2AACA0YgdAABgNGIHAAAYjdgBAABGI3YAAIDRiB0AAGA0YgcAABiN2AEAAEYjdgAAgNGIHQAAYDRiBwAAGI3YAQAARiN2AACA0YgdAABgNGIHAAAYjdgBAABGI3YAAIDRiB0AAGA0YgcAABiN2AEAAEYjdgAAgNGIHQAAYDRiBwAAGI3YAQAARiN2AACA0YgdAABgNGIHAAAYjdgBAABGI3YAAIDRiB0AAGA0YgcAABiN2AEAAEYLaewsXrxYDocjaPN4PPZ+y7K0ePFiJSQkKDo6WiNGjNDhw4eDjhEIBJSfn6/evXurR48eeuihh3Ty5MkbfSoAACBMhfzKzt133626ujp7O3jwoL1v+fLlWrlypdasWaOqqip5PB6NHj1ajY2N9pyCggJt3bpVZWVl2r17t06fPq0xY8aopaUlFKcDAADCTGTIFxAZGXQ15wLLsrR69WotWLBA48aNkyRt2LBBbrdbW7Zs0dSpU+Xz+bRu3Tpt2rRJmZmZkqTNmzcrMTFRO3fuVHZ29g09FwAAEH5CfmXnww8/VEJCgpKSkvSDH/xAH330kSSppqZGXq9XWVlZ9lyn06mMjAxVVlZKkqqrq3Xu3LmgOQkJCUpJSbHnXE4gEJDf7w/aAACAmUIaO0OGDNHGjRu1fft2lZSUyOv1Kj09XZ999pm8Xq8kye12Bz3H7Xbb+7xer6KiotSrV68rzrmcoqIiuVwue0tMTGznMwMAAOEipLGTk5Oj73//+0pNTVVmZqbeeOMNSf/3dtUFDocj6DmWZV0ydrGvmjN//nz5fD57q62tvY6zAAAA4Szkb2P9rR49eig1NVUffvihfR/PxVdo6uvr7as9Ho9Hzc3NamhouOKcy3E6nYqNjQ3aAACAmcIqdgKBgI4ePap+/fopKSlJHo9H5eXl9v7m5mZVVFQoPT1dkpSWlqauXbsGzamrq9OhQ4fsOQAA4OYW0k9jzZ49W2PHjtVtt92m+vp6Pfvss/L7/Zo8ebIcDocKCgpUWFio5ORkJScnq7CwUN27d9eECRMkSS6XS1OmTNGsWbMUHx+vuLg4zZ49235bDAAAIKSxc/LkSY0fP16nTp1Snz599Pd///fau3evBgwYIEmaM2eOmpqalJeXp4aGBg0ZMkQ7duxQTEyMfYxVq1YpMjJSubm5ampq0qhRo1RaWqqIiIhQnRYAAAgjDsuyrFAvItT8fr9cLpd8Pl+H3r+T9tTGDjs20FlVr3g01EsA0Eld7e/vsLpnBwAAoL0ROwAAwGjEDgAAMBqxAwAAjEbsAAAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGjEDgAAMBqxAwAAjEbsAAAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGjEDgAAMBqxAwAAjEbsAAAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGjEDgAAMBqxAwAAjEbsAAAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGhhEztFRUVyOBwqKCiwxyzL0uLFi5WQkKDo6GiNGDFChw8fDnpeIBBQfn6+evfurR49euihhx7SyZMnb/DqAQBAuAqL2KmqqtLatWt1zz33BI0vX75cK1eu1Jo1a1RVVSWPx6PRo0ersbHRnlNQUKCtW7eqrKxMu3fv1unTpzVmzBi1tLTc6NMAAABhKOSxc/r0aU2cOFElJSXq1auXPW5ZllavXq0FCxZo3LhxSklJ0YYNG3T27Flt2bJFkuTz+bRu3To9//zzyszM1ODBg7V582YdPHhQO3fuDNUpAQCAMBLy2HniiSf0j//4j8rMzAwar6mpkdfrVVZWlj3mdDqVkZGhyspKSVJ1dbXOnTsXNCchIUEpKSn2nMsJBALy+/1BGwAAMFNkKH94WVmZ3n//fVVVVV2yz+v1SpLcbnfQuNvt1p///Gd7TlRUVNAVoQtzLjz/coqKirRkyZLrXT4AAOgEQnZlp7a2Vj/5yU+0efNmdevW7YrzHA5H0GPLsi4Zu9hXzZk/f758Pp+91dbWXtviAQBApxGy2KmurlZ9fb3S0tIUGRmpyMhIVVRU6MUXX1RkZKR9RefiKzT19fX2Po/Ho+bmZjU0NFxxzuU4nU7FxsYGbQAAwEwhi51Ro0bp4MGDOnDggL098MADmjhxog4cOKCBAwfK4/GovLzcfk5zc7MqKiqUnp4uSUpLS1PXrl2D5tTV1enQoUP2HAAAcHML2T07MTExSklJCRrr0aOH4uPj7fGCggIVFhYqOTlZycnJKiwsVPfu3TVhwgRJksvl0pQpUzRr1izFx8crLi5Os2fPVmpq6iU3PAMAgJtTSG9Q/ipz5sxRU1OT8vLy1NDQoCFDhmjHjh2KiYmx56xatUqRkZHKzc1VU1OTRo0apdLSUkVERIRw5QAAIFw4LMuyQr2IUPP7/XK5XPL5fB16/07aUxs77NhAZ1W94tFQLwFAJ3W1v79D/j07AAAAHYnYAQAARiN2AACA0YgdAABgNGIHAAAYjdgBAABGI3YAAIDRiB0AAGA0YgcAABiN2AEAAEYjdgAAgNGIHQAAYDRiBwAAGI3YAQAARiN2AACA0YgdAABgNGIHAAAYjdgBAABGI3YAAIDRiB0AAGA0YgcAABiN2AEAAEYjdgAAgNGIHQAAYDRiBwAAGI3YAQAARiN2AACA0YgdAABgNGIHAAAYjdgBAABGI3YAAIDRiB0AAGA0YgcAABiN2AEAAEYjdgAAgNHaFDsjR47U559/fsm43+/XyJEjr3dNAAAA7aZNsbNr1y41NzdfMv7FF1/o3Xffve5FAQAAtJfIa5n8hz/8wf7nI0eOyOv12o9bWlq0bds23Xrrre23OgAAgOt0TbFz3333yeFwyOFwXPbtqujoaL300kvttjgAAIDrdU2xU1NTI8uyNHDgQO3bt099+vSx90VFRalv376KiIho90UCAAC01TXFzoABAyRJra2tHbIYAACA9nZNsfO3/vjHP2rXrl2qr6+/JH4WLVp03QsDAABoD22KnZKSEv34xz9W79695fF45HA47H0Oh4PYAQAAYaNNsfPss8/queee09y5c9t7PQAAAO2qTd+z09DQoIcffri91wIAANDu2nRl5+GHH9aOHTs0bdq09l4PAHRKJ5amhnoJQNi5bdHBUC9BUhtj5/bbb9fChQu1d+9epaamqmvXrkH7p0+f3i6LAwAAuF5tip21a9eqZ8+eqqioUEVFRdA+h8NB7AAAgLDRptipqalp73UAAAB0iDbdoAwAANBZtOnKzuOPP/6l+3/+859f1XGKi4tVXFysjz/+WJJ09913a9GiRcrJyZEkWZalJUuWaO3atWpoaNCQIUP0H//xH7r77rvtYwQCAc2ePVu/+MUv1NTUpFGjRunll19W//7923JqAADAMG3+6PnfbvX19frtb3+rX/3qV/r888+v+jj9+/fXT3/6U+3fv1/79+/XyJEj9Z3vfEeHDx+WJC1fvlwrV67UmjVrVFVVJY/Ho9GjR6uxsdE+RkFBgbZu3aqysjLt3r1bp0+f1pgxY9TS0tKWUwMAAIZp05WdrVu3XjLW2tqqvLw8DRw48KqPM3bs2KDHzz33nIqLi7V3717dddddWr16tRYsWKBx48ZJkjZs2CC3260tW7Zo6tSp8vl8WrdunTZt2qTMzExJ0ubNm5WYmKidO3cqOzu7LacHAAAM0m737HTp0kUzZszQqlWr2vT8lpYWlZWV6cyZMxo6dKhqamrk9XqVlZVlz3E6ncrIyFBlZaUkqbq6WufOnQuak5CQoJSUFHvO5QQCAfn9/qANAACYqV1vUD5+/LjOnz9/Tc85ePCgevbsKafTqWnTpmnr1q2666675PV6JUlutztovtvttvd5vV5FRUWpV69eV5xzOUVFRXK5XPaWmJh4TWsGAACdR5vexpo5c2bQY8uyVFdXpzfeeEOTJ0++pmPdeeedOnDggD7//HO9/vrrmjx5ctB39/ztHxm98LMuHrvYV82ZP39+0Dn4/X6CBwAAQ7Updj744IOgx126dFGfPn30/PPPf+UntS4WFRWl22+/XZL0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"/>


```python
# x 파라미터를 class로 변경해서 
#'선실 등급별 빈도 막대 그래프'를 만들어라

sns.countplot(data = df, x = 'class')
```

<pre>
<Axes: xlabel='class', ylabel='count'>
</pre>
<img src="data:image/png;base64,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"/>


```python
# x 파라미터를 class로 지정하고, hue 파라미터에 alive 변수를 지정해서
# '선실 등급별 생존 여부를 나타내는 막대 그래프'를 만들어라
# cf) hue : 변수 항목별로 막대의 색을 다르게 표현하는 파라미터

sns.countplot(data = df, x = 'class', hue = 'alive')
```

<pre>
<Axes: xlabel='class', ylabel='count'>
</pre>
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAjsAAAGwCAYAAABPSaTdAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjcuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8pXeV/AAAACXBIWXMAAA9hAAAPYQGoP6dpAAA07klEQVR4nO3deXQV9f3/8dcly01CFkhCcm9KiCBLwQSVgBiqrGFJWYUCKr8CZSkWwaZAsegBg1Ui8AVc+JZSimGTglVjsSISoIlFpIUcowgU0AaBkpgKIWEJNxDm94df5nhlEULCXIbn45w5h/l8PjP3/YlX8uIzc+c6DMMwBAAAYFN1rC4AAACgNhF2AACArRF2AACArRF2AACArRF2AACArRF2AACArRF2AACArflbXYAvuHDhgo4ePaqwsDA5HA6rywEAANfAMAydPHlScXFxqlPnyus3hB1JR48eVXx8vNVlAACAajh8+LAaNmx4xX7CjqSwsDBJ3/ywwsPDLa4GAABci/LycsXHx5u/x6+EsCOZl67Cw8MJOwAA3GK+7xYUblAGAAC2RtgBAAC2RtgBAAC2xj07AABYrKqqSufOnbO6DJ8TEBAgPz+/Gz4PYQcAAIsYhqHi4mKdOHHC6lJ8Vr169eRyuW7oOXiEHQAALHIx6MTExCgkJIQH236LYRg6c+aMSkpKJElut7va5yLsAABggaqqKjPoREVFWV2OTwoODpYklZSUKCYmptqXtLhBGQAAC1y8RyckJMTiSnzbxZ/PjdzTRNgBAMBCXLq6upr4+RB2AACArRF2AACArRF2AAC4jRw8eFAOh0MFBQWSpNzcXDkcDlt//J2wAwDAbaxDhw4qKipSRESE1aXUGj56DgDAbSwwMFAul8vqMmoVKzsAANjMhg0b9MADD6hevXqKiopSnz599MUXX1x27LcvY5WVlSk4OFgbNmzwGvPWW2+pbt26OnXqlCTpP//5j4YOHar69esrKipK/fv318GDB2t7WtXGyg4A4KZJ/vUKq0vwCflzh9fq+U+fPq1JkyYpKSlJp0+f1owZM/TQQw+Z9+lcSUREhHr37q3XXntNvXr1MttXr16t/v37KzQ0VGfOnFGXLl304IMP6oMPPpC/v7+ee+459erVS59++qkCAwNrdW7VQdgBAMBmBg0a5LW/dOlSxcTEaM+ePQoNDb3qscOGDdPw4cN15swZhYSEqLy8XO+++67efPNNSdKaNWtUp04d/fGPfzSfgZOVlaV69eopNzdXPXr0qJ1J3QAuYwEAYDNffPGFHn30UTVp0kTh4eFq3LixJOnQoUPfe2zv3r3l7++vdevWSZLefPNNhYWFmSEmPz9fn3/+ucLCwhQaGqrQ0FBFRkbq7NmzV7xUZjVWdgAAsJm+ffsqPj5eS5YsUVxcnC5cuKDExERVVlZ+77GBgYH6yU9+otWrV+vhhx/W6tWrNXToUPn7fxMZLly4oOTkZL322muXHNugQYMan0tNIOwAAGAjx44d0969e7V48WI9+OCDkqStW7de1zmGDRumHj16aPfu3frb3/6m3/72t2ZfmzZttHbtWsXExCg8PLxGa68tXMYCAMBGLn5C6g9/+IM+//xzbdmyRZMmTbquc3Tq1EmxsbEaNmyY7rjjDt1///1m37BhwxQdHa3+/fvr73//uwoLC5WXl6df/vKXOnLkSE1Pp0YQdgAAsJE6depozZo1ys/PV2Jion71q19p7ty513UOh8OhRx55RJ988omGDRvm1RcSEqIPPvhAjRo10sCBA9WyZUuNGjVKFRUVPrvS4zAMw7C6CKuVl5crIiJCZWVlPvsfCgDsgI+efyN/7nCdPXtWhYWFaty4sYKCgqwuyWdd7ed0rb+/WdkBAAC2RtgBAAC2RtgBAAC2RtgBAAC2RtgBAAC2RtgBAAC2RtgBAAC2RtgBAAC2RtgBAAC2ZukXgS5atEiLFi3SwYMHJUl33XWXZsyYobS0NEnSyJEjtXz5cq9j2rdvr+3bt5v7Ho9HU6ZM0Z/+9CdVVFSoW7du+t3vfqeGDRvetHkAAFCTbuaTpvPnDr9pr2UVS1d2GjZsqBdeeEE7d+7Uzp071bVrV/Xv31+7d+82x/Tq1UtFRUXmtn79eq9zpKenKzs7W2vWrNHWrVt16tQp9enTR1VVVTd7OgAAwAdZGnb69u2rH//4x2revLmaN2+u559/XqGhoV4rN06nUy6Xy9wiIyPNvrKyMi1dulTz5s1Tamqq7r33Xq1atUq7du3Spk2brJgSAAC217lzZz3xxBOaOnWqIiMj5XK5lJGRYfYfOnRI/fv3V2hoqMLDwzVkyBB99dVXltXrM/fsVFVVac2aNTp9+rRSUlLM9tzcXMXExKh58+YaO3asSkpKzL78/HydO3dOPXr0MNvi4uKUmJiobdu2XfG1PB6PysvLvTYAAHDtli9frrp16+of//iH5syZo2effVY5OTkyDEMDBgzQ8ePHlZeXp5ycHH3xxRcaOnSoZbVaes+OJO3atUspKSk6e/asQkNDlZ2drVatWkmS0tLSNHjwYCUkJKiwsFDTp09X165dlZ+fL6fTqeLiYgUGBqp+/fpe54yNjVVxcfEVXzMzM1MzZ86s1XkBAGBnrVu31jPPPCNJatasmRYuXKjNmzdLkj799FMVFhYqPj5ekrRy5Urddddd2rFjh9q1a3fTa7V8ZadFixYqKCjQ9u3b9Ytf/EIjRozQnj17JElDhw5V7969lZiYqL59++q9997T/v379e677171nIZhyOFwXLF/2rRpKisrM7fDhw/X6JwAALC71q1be+273W6VlJRo7969io+PN4OOJLVq1Ur16tXT3r17b3aZknxgZScwMFBNmzaVJLVt21Y7duzQSy+9pMWLF18y1u12KyEhQQcOHJAkuVwuVVZWqrS01Gt1p6SkRB06dLjiazqdTjmdzhqeCQAAt4+AgACvfYfDoQsXLlxxweH7FiJqk+UrO99lGIY8Hs9l+44dO6bDhw/L7XZLkpKTkxUQEKCcnBxzTFFRkT777LOrhh0AAFA7WrVqpUOHDnldNdmzZ4/KysrUsmVLS2qydGXnqaeeUlpamuLj43Xy5EmtWbNGubm52rBhg06dOqWMjAwNGjRIbrdbBw8e1FNPPaXo6Gg99NBDkqSIiAiNHj1akydPVlRUlCIjIzVlyhQlJSUpNTXVyqkBAHBbSk1NVevWrTVs2DC9+OKLOn/+vMaPH69OnTqpbdu2ltRkadj56quv9NOf/lRFRUWKiIhQ69attWHDBnXv3l0VFRXatWuXVqxYoRMnTsjtdqtLly5au3atwsLCzHMsWLBA/v7+GjJkiPlQwWXLlsnPz8/CmQEAcHtyOBx6++23NXHiRHXs2FF16tRRr1699Morr1hXk2EYhmWv7iPKy8sVERGhsrIyhYeHW10OANjWzXwysC/LnztcZ8+eVWFhoRo3bqygoCCrS/JZV/s5Xevvb5+7ZwcAAKAmEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtWfrdWAAA4FKHnk26aa/VaMaum/ZaVmFlBwAA2BphBwAAXLMVK1YoKipKHo/Hq33QoEEaPny4JOmdd95RcnKygoKC1KRJE82cOVPnz583x2ZkZKhRo0ZyOp2Ki4vTE088Uas1E3YAAMA1Gzx4sKqqqrRu3Tqz7euvv9Zf//pX/exnP9P777+v//f//p+eeOIJ7dmzR4sXL9ayZcv0/PPPS5LeeOMNLViwQIsXL9aBAwf09ttvKympdi/bEXYAAMA1Cw4O1qOPPqqsrCyz7bXXXlPDhg3VuXNnPf/88/rNb36jESNGqEmTJurevbt++9vfavHixZKkQ4cOyeVyKTU1VY0aNdJ9992nsWPH1mrNhB0AAHBdxo4dq40bN+o///mPJCkrK0sjR46Uw+FQfn6+nn32WYWGhprb2LFjVVRUpDNnzmjw4MGqqKhQkyZNNHbsWGVnZ3td4qoNfBoLAABcl3vvvVd33323VqxYoZ49e2rXrl165513JEkXLlzQzJkzNXDgwEuOCwoKUnx8vPbt26ecnBxt2rRJ48eP19y5c5WXl6eAgIBaqZewAwAArtuYMWO0YMEC/ec//1Fqaqri4+MlSW3atNG+ffvUtGnTKx4bHBysfv36qV+/fnr88cf1wx/+ULt27VKbNm1qpVbCDgAAuG7Dhg3TlClTtGTJEq1YscJsnzFjhvr06aP4+HgNHjxYderU0aeffqpdu3bpueee07Jly1RVVaX27dsrJCREK1euVHBwsBISEmqtVu7ZAQAA1y08PFyDBg1SaGioBgwYYLb37NlTf/3rX5WTk6N27drp/vvv1/z5880wU69ePS1ZskQ/+tGP1Lp1a23evFnvvPOOoqKiaq1WVnYAAPAxt8pTjYuKijRs2DA5nU6v9p49e6pnz56XPWbAgAFe4ehmIOwAAIDrcvz4cW3cuFFbtmzRwoULrS7nexF2AADAdWnTpo1KS0s1e/ZstWjRwupyvhdhBwAAXJeDBw9aXcJ14QZlAABga4QdAAAsZBiG1SX4tJr4+RB2AACwwMWnBZ85c8biSnzbxZ/PjTxdmXt2AACwgJ+fn+rVq6eSkhJJUkhIiBwOh8VV+Q7DMHTmzBmVlJSoXr168vPzq/a5CDsAAFjE5XJJkhl4cKl69eqZP6fqIuwAAGARh8Mht9utmJgYnTt3zupyfE5AQMANrehcRNgBAMBifn5+NfJLHZfHDcoAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWLA07ixYtUuvWrRUeHq7w8HClpKTovffeM/sNw1BGRobi4uIUHByszp07a/fu3V7n8Hg8mjhxoqKjo1W3bl3169dPR44cudlTAQAAPsrSsNOwYUO98MIL2rlzp3bu3KmuXbuqf//+ZqCZM2eO5s+fr4ULF2rHjh1yuVzq3r27Tp48aZ4jPT1d2dnZWrNmjbZu3apTp06pT58+qqqqsmpaAADAhzgMH/sGssjISM2dO1ejRo1SXFyc0tPT9eSTT0r6ZhUnNjZWs2fP1rhx41RWVqYGDRpo5cqVGjp0qCTp6NGjio+P1/r169WzZ89res3y8nJFRESorKxM4eHhtTY3ALjdJf96hdUl+IT8ucOtLsEWrvX3t8/cs1NVVaU1a9bo9OnTSklJUWFhoYqLi9WjRw9zjNPpVKdOnbRt2zZJUn5+vs6dO+c1Ji4uTomJieaYy/F4PCovL/faAACAPVkednbt2qXQ0FA5nU499thjys7OVqtWrVRcXCxJio2N9RofGxtr9hUXFyswMFD169e/4pjLyczMVEREhLnFx8fX8KwAAICvsDzstGjRQgUFBdq+fbt+8YtfaMSIEdqzZ4/Z/91vgDUM43u/Ffb7xkybNk1lZWXmdvjw4RubBAAA8FmWh53AwEA1bdpUbdu2VWZmpu6++2699NJL5jecfneFpqSkxFztcblcqqysVGlp6RXHXI7T6TQ/AXZxAwAA9mR52PkuwzDk8XjUuHFjuVwu5eTkmH2VlZXKy8tThw4dJEnJyckKCAjwGlNUVKTPPvvMHAMAAG5vln7r+VNPPaW0tDTFx8fr5MmTWrNmjXJzc7VhwwY5HA6lp6dr1qxZatasmZo1a6ZZs2YpJCREjz76qCQpIiJCo0eP1uTJkxUVFaXIyEhNmTJFSUlJSk1NtXJqAADAR1gadr766iv99Kc/VVFRkSIiItS6dWtt2LBB3bt3lyRNnTpVFRUVGj9+vEpLS9W+fXtt3LhRYWFh5jkWLFggf39/DRkyRBUVFerWrZuWLVsmPz8/q6YFAAB8iM89Z8cKPGcHAG4OnrPzDZ6zUzNuuefsAAAA1AbCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDVLw05mZqbatWunsLAwxcTEaMCAAdq3b5/XmJEjR8rhcHht999/v9cYj8ejiRMnKjo6WnXr1lW/fv105MiRmzkVAADgoywNO3l5eXr88ce1fft25eTk6Pz58+rRo4dOnz7tNa5Xr14qKioyt/Xr13v1p6enKzs7W2vWrNHWrVt16tQp9enTR1VVVTdzOgAAwAf5W/niGzZs8NrPyspSTEyM8vPz1bFjR7Pd6XTK5XJd9hxlZWVaunSpVq5cqdTUVEnSqlWrFB8fr02bNqlnz56XHOPxeOTxeMz98vLympgOAADwQT51z05ZWZkkKTIy0qs9NzdXMTExat68ucaOHauSkhKzLz8/X+fOnVOPHj3Mtri4OCUmJmrbtm2XfZ3MzExFRESYW3x8fC3MBgAA+AKfCTuGYWjSpEl64IEHlJiYaLanpaXptdde05YtWzRv3jzt2LFDXbt2NVdmiouLFRgYqPr163udLzY2VsXFxZd9rWnTpqmsrMzcDh8+XHsTAwAAlrL0Mta3TZgwQZ9++qm2bt3q1T506FDzz4mJiWrbtq0SEhL07rvvauDAgVc8n2EYcjgcl+1zOp1yOp01UzgAAPBpPrGyM3HiRK1bt05/+9vf1LBhw6uOdbvdSkhI0IEDByRJLpdLlZWVKi0t9RpXUlKi2NjYWqsZAADcGiwNO4ZhaMKECXrrrbe0ZcsWNW7c+HuPOXbsmA4fPiy32y1JSk5OVkBAgHJycswxRUVF+uyzz9ShQ4daqx0AANwaLL2M9fjjj2v16tX6y1/+orCwMPMem4iICAUHB+vUqVPKyMjQoEGD5Ha7dfDgQT311FOKjo7WQw89ZI4dPXq0Jk+erKioKEVGRmrKlClKSkoyP50FAABuX5aGnUWLFkmSOnfu7NWelZWlkSNHys/PT7t27dKKFSt04sQJud1udenSRWvXrlVYWJg5fsGCBfL399eQIUNUUVGhbt26admyZfLz87uZ0wEAAD7IYRiGYXURVisvL1dERITKysoUHh5udTkAYFvJv15hdQk+IX/ucKtLsIVr/f3tEzcoAwAA1BbCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsDXCDgAAsLVqhZ2uXbvqxIkTl7SXl5era9euN1oTAABAjalW2MnNzVVlZeUl7WfPntXf//73Gy4KAACgpvhfz+BPP/3U/POePXtUXFxs7ldVVWnDhg36wQ9+UHPVAQAA3KDrCjv33HOPHA6HHA7HZS9XBQcH65VXXqmx4gAAAG7UdYWdwsJCGYahJk2a6J///KcaNGhg9gUGBiomJkZ+fn41XiQAAEB1XVfYSUhIkCRduHChVooBAACoadcVdr5t//79ys3NVUlJySXhZ8aMGTdcGAAAQE2oVthZsmSJfvGLXyg6Oloul0sOh8PsczgchB0AAOAzqhV2nnvuOT3//PN68skna7oeAACAGlWt5+yUlpZq8ODBN/zimZmZateuncLCwhQTE6MBAwZo3759XmMMw1BGRobi4uIUHByszp07a/fu3V5jPB6PJk6cqOjoaNWtW1f9+vXTkSNHbrg+AABw66tW2Bk8eLA2btx4wy+el5enxx9/XNu3b1dOTo7Onz+vHj166PTp0+aYOXPmaP78+Vq4cKF27Nghl8ul7t276+TJk+aY9PR0ZWdna82aNdq6datOnTqlPn36qKqq6oZrBAAAt7ZqXcZq2rSppk+fru3btyspKUkBAQFe/U888cQ1nWfDhg1e+1lZWYqJiVF+fr46duwowzD04osv6umnn9bAgQMlScuXL1dsbKxWr16tcePGqaysTEuXLtXKlSuVmpoqSVq1apXi4+O1adMm9ezZ85LX9Xg88ng85n55efl1zR8AANw6qhV2/vCHPyg0NFR5eXnKy8vz6nM4HNccdr6rrKxMkhQZGSnpm+f6FBcXq0ePHuYYp9OpTp06adu2bRo3bpzy8/N17tw5rzFxcXFKTEzUtm3bLht2MjMzNXPmzGrVCAAAbi3VCjuFhYU1XYcMw9CkSZP0wAMPKDExUZLMr6OIjY31GhsbG6svv/zSHBMYGKj69etfMubbX2fxbdOmTdOkSZPM/fLycsXHx9fYXAAAgO+o9nN2atqECRP06aefauvWrZf0ffuj7dI3wei7bd91tTFOp1NOp7P6xQIAgFtGtcLOqFGjrtr/6quvXtf5Jk6cqHXr1umDDz5Qw4YNzXaXyyXpm9Ubt9tttpeUlJirPS6XS5WVlSotLfVa3SkpKVGHDh2uqw4AAGA/1f7o+be3kpISbdmyRW+99ZZOnDhxzecxDEMTJkzQW2+9pS1btqhx48Ze/Y0bN5bL5VJOTo7ZVllZqby8PDPIJCcnKyAgwGtMUVGRPvvsM8IOAACo3spOdnb2JW0XLlzQ+PHj1aRJk2s+z+OPP67Vq1frL3/5i8LCwsx7bCIiIhQcHCyHw6H09HTNmjVLzZo1U7NmzTRr1iyFhITo0UcfNceOHj1akydPVlRUlCIjIzVlyhQlJSWZn84CAAC3rxq7Z6dOnTr61a9+pc6dO2vq1KnXdMyiRYskSZ07d/Zqz8rK0siRIyVJU6dOVUVFhcaPH6/S0lK1b99eGzduVFhYmDl+wYIF8vf315AhQ1RRUaFu3bpp2bJlfAM7AACQwzAMo6ZOtn79eo0YMUL//e9/a+qUN0V5ebkiIiJUVlam8PBwq8sBANtK/vUKq0vwCflzh1tdgi1c6+/vaq3sfPtj29I3994UFRXp3Xff1YgRI6pzSgAAgFpRrbDz8ccfe+3XqVNHDRo00Lx58773k1oAAAA3U7XCzt/+9reargMAAKBW3NANyv/973+1b98+ORwONW/eXA0aNKipugAAAGpEtZ6zc/r0aY0aNUput1sdO3bUgw8+qLi4OI0ePVpnzpyp6RoBAACqrVphZ9KkScrLy9M777yjEydO6MSJE/rLX/6ivLw8TZ48uaZrBAAAqLZqXcZ688039cYbb3g9H+fHP/6xgoODNWTIEPP5OQAAAFar1srOmTNnLvkmckmKiYnhMhYAAPAp1Qo7KSkpeuaZZ3T27FmzraKiQjNnzlRKSkqNFQcAAHCjqnUZ68UXX1RaWpoaNmyou+++Ww6HQwUFBXI6ndq4cWNN1wgAAFBt1Qo7SUlJOnDggFatWqV//etfMgxDDz/8sIYNG6bg4OCarhEAAKDaqhV2MjMzFRsbq7Fjx3q1v/rqq/rvf/+rJ598skaKAwAAuFHVumdn8eLF+uEPf3hJ+1133aXf//73N1wUAABATalW2CkuLpbb7b6kvUGDBioqKrrhogAAAGpKtcJOfHy8Pvzww0vaP/zwQ8XFxd1wUQAAADWlWvfsjBkzRunp6Tp37py6du0qSdq8ebOmTp3KE5QBAIBPqVbYmTp1qo4fP67x48ersrJSkhQUFKQnn3xS06ZNq9ECAQAAbkS1wo7D4dDs2bM1ffp07d27V8HBwWrWrJmcTmdN1wcAAHBDqhV2LgoNDVW7du1qqhYAAIAaV60blAEAAG4VhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrhB0AAGBrloadDz74QH379lVcXJwcDofefvttr/6RI0fK4XB4bffff7/XGI/Ho4kTJyo6Olp169ZVv379dOTIkZs4CwAA4MssDTunT5/W3XffrYULF15xTK9evVRUVGRu69ev9+pPT09Xdna21qxZo61bt+rUqVPq06ePqqqqart8AABwC/C38sXT0tKUlpZ21TFOp1Mul+uyfWVlZVq6dKlWrlyp1NRUSdKqVasUHx+vTZs2qWfPnjVeMwAAuLX4/D07ubm5iomJUfPmzTV27FiVlJSYffn5+Tp37px69OhhtsXFxSkxMVHbtm274jk9Ho/Ky8u9NgAAYE8+HXbS0tL02muvacuWLZo3b5527Nihrl27yuPxSJKKi4sVGBio+vXrex0XGxur4uLiK543MzNTERER5hYfH1+r8wAAANax9DLW9xk6dKj558TERLVt21YJCQl69913NXDgwCseZxiGHA7HFfunTZumSZMmmfvl5eUEHgAAbMqnV3a+y+12KyEhQQcOHJAkuVwuVVZWqrS01GtcSUmJYmNjr3gep9Op8PBwrw0AANjTLRV2jh07psOHD8vtdkuSkpOTFRAQoJycHHNMUVGRPvvsM3Xo0MGqMgEAgA+x9DLWqVOn9Pnnn5v7hYWFKigoUGRkpCIjI5WRkaFBgwbJ7Xbr4MGDeuqppxQdHa2HHnpIkhQREaHRo0dr8uTJioqKUmRkpKZMmaKkpCTz01kAAOD2ZmnY2blzp7p06WLuX7yPZsSIEVq0aJF27dqlFStW6MSJE3K73erSpYvWrl2rsLAw85gFCxbI399fQ4YMUUVFhbp166Zly5bJz8/vps8HAAD4HodhGIbVRVitvLxcERERKisr4/4dAKhFyb9eYXUJPiF/7nCrS7CFa/39fUvdswMAAHC9CDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWCDsAAMDWfPq7sXBrOvRsktUl+IRGM3ZZXQIAQKzsAAAAmyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAWyPsAAAAW/O3ugAAAG43h55NsroEn9Boxq6b8jqs7AAAAFsj7AAAAFsj7AAAAFsj7AAAAFsj7AAAAFsj7AAAAFsj7AAAAFsj7AAAAFsj7AAAAFsj7AAAAFsj7AAAAFsj7AAAAFsj7AAAAFuzNOx88MEH6tu3r+Li4uRwOPT222979RuGoYyMDMXFxSk4OFidO3fW7t27vcZ4PB5NnDhR0dHRqlu3rvr166cjR47cxFkAAABfZmnYOX36tO6++24tXLjwsv1z5szR/PnztXDhQu3YsUMul0vdu3fXyZMnzTHp6enKzs7WmjVrtHXrVp06dUp9+vRRVVXVzZoGAADwYf5WvnhaWprS0tIu22cYhl588UU9/fTTGjhwoCRp+fLlio2N1erVqzVu3DiVlZVp6dKlWrlypVJTUyVJq1atUnx8vDZt2qSePXvetLkAAADf5LP37BQWFqq4uFg9evQw25xOpzp16qRt27ZJkvLz83Xu3DmvMXFxcUpMTDTHXI7H41F5ebnXBgAA7Mlnw05xcbEkKTY21qs9NjbW7CsuLlZgYKDq169/xTGXk5mZqYiICHOLj4+v4eoBAICv8Nmwc5HD4fDaNwzjkrbv+r4x06ZNU1lZmbkdPny4RmoFAAC+x2fDjsvlkqRLVmhKSkrM1R6Xy6XKykqVlpZecczlOJ1OhYeHe20AAMCeLL1B+WoaN24sl8ulnJwc3XvvvZKkyspK5eXlafbs2ZKk5ORkBQQEKCcnR0OGDJEkFRUV6bPPPtOcOXMsqx3wFcm/XmF1CT4hf+5wq0sAYCFLw86pU6f0+eefm/uFhYUqKChQZGSkGjVqpPT0dM2aNUvNmjVTs2bNNGvWLIWEhOjRRx+VJEVERGj06NGaPHmyoqKiFBkZqSlTpigpKcn8dBYAALi9WRp2du7cqS5dupj7kyZNkiSNGDFCy5Yt09SpU1VRUaHx48ertLRU7du318aNGxUWFmYes2DBAvn7+2vIkCGqqKhQt27dtGzZMvn5+d30+QAAAN9jadjp3LmzDMO4Yr/D4VBGRoYyMjKuOCYoKEivvPKKXnnllVqoEAAA3Op89gZlAACAmkDYAQAAtkbYAQAAtkbYAQAAtkbYAQAAtuazDxUEgJpy6Nkkq0vwCY1m7LK6BMASrOwAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABbI+wAAABb46PnNST51yusLsFnZId9/xgAAG4WVnYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICtEXYAAICt+XTYycjIkMPh8NpcLpfZbxiGMjIyFBcXp+DgYHXu3Fm7d++2sGIAAOBrfDrsSNJdd92loqIic9u1a5fZN2fOHM2fP18LFy7Ujh075HK51L17d508edLCigEAgC/xt7qA7+Pv7++1mnORYRh68cUX9fTTT2vgwIGSpOXLlys2NlarV6/WuHHjrnhOj8cjj8dj7peXl9d84QAAwCf4/MrOgQMHFBcXp8aNG+vhhx/Wv//9b0lSYWGhiouL1aNHD3Os0+lUp06dtG3btqueMzMzUxEREeYWHx9fq3MAAADW8emw0759e61YsULvv/++lixZouLiYnXo0EHHjh1TcXGxJCk2NtbrmNjYWLPvSqZNm6aysjJzO3z4cK3NAQAAWMunL2OlpaWZf05KSlJKSoruvPNOLV++XPfff78kyeFweB1jGMYlbd/ldDrldDprvmAAAOBzfHpl57vq1q2rpKQkHThwwLyP57urOCUlJZes9gAAgNvXLRV2PB6P9u7dK7fbrcaNG8vlciknJ8fsr6ysVF5enjp06GBhlQAAwJf49GWsKVOmqG/fvmrUqJFKSkr03HPPqby8XCNGjJDD4VB6erpmzZqlZs2aqVmzZpo1a5ZCQkL06KOPWl06AADwET4ddo4cOaJHHnlEX3/9tRo0aKD7779f27dv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+Pzzz80x//u//2vExsaa+26323jhhRfM/XPnzhkNGzY0+vfvf2OTxy0rKyvLiIiIuKS9sLDQkGT88Y9/NNt2795tSDL27t172WOfeeYZIyAgwCgpKTHb3n//fcPPz884fPiw2fbee+/x92c1sLKDq+rSpYsKCgrM7eWXX77suG//K1r65l/SBQUFatGihZ544glt3LjxZpSLW9SgQYN09OhRrVu3Tj179lRubq7atGmjZcuWKT8/X6dOnVJUVJS5ChQaGqrCwkJ98cUXkqSCggJ169btsufeu3ev/P391b59e7MtKipKLVq00N69e822kJAQ3Xnnnea+2+1WSUmJpG8uoxUVFSklJcXs9/f3v+R9D3xb69atzT+73W5JMt9Tl5OQkKAGDRqY+3v37lWjRo3UsGFDs+3b70FcO25QxlXVrVtXTZs2vaZx39amTRsVFhbqvffe06ZNmzRkyBClpqbqjTfeqK1ScYsLCgpS9+7d1b17d82YMUNjxozRM888o/Hjx8vtdis3N/eSYy7e83C1Gz2NK9xXYxiGHA6Huf/dm0EdDgf35OCGfPs9dfG9duHChSuO/+7fo5d7/337PYtrx8oOak14eLiGDh2qJUuWaO3atXrzzTfNeywCAgJUVVVlcYXwZa1atdLp06fVpk0bFRcXy9/fX02bNvXaoqOjJX3zL+jNmzdf8Tznz5/XP/7xD7Pt2LFj2r9/v1q2bHlNtURERMjtdmv79u1m2/nz55Wfn38DMwSurlWrVjp06JCOHj1qtvE4huphZQe1YsGCBXK73brnnntUp04d/fnPf5bL5TL/JX7HHXdo8+bN+tGPfiSn06n69etbWzAsc+zYMQ0ePFijRo1S69atFRYWpp07d2rOnDnq37+/UlNTlZKSogEDBmj27Nlq0aKFjh49qvXr12vAgAFq27atnnnmGXXr1k133nmnHn74YZ0/f17vvfeepk6dqmbNmql///4aO3asFi9erLCwMP3mN7/RD37wA/Xv3/+a6/zlL3+pF154Qc2aNVPLli01f/58nThxovZ+MLjtpaamqkWLFho+fLjmzZun8vJyPf3001aXdUtiZQe1IjQ0VLNnz1bbtm3Vrl07HTx4UOvXr1edOt+85ebNm6ecnBzFx8fr3nvvtbhaWCk0NFTt27fXggUL1LFjRyUmJmr69OkaO3asFi5cKIfDofXr16tjx44aNWqUmjdvrocfflgHDx5UbGyspG+e6v3nP/9Z69at0z333KOuXbt6reRkZWUpOTlZffr0UUpKigzD0Pr166/rOSaTJ0/W8OHDNXLkSKWkpCgsLEwPPfRQjf88gIvq1Kmj7OxseTwe3XfffRozZoyef/55q8u6JTkMLkoDAAAbY2UHAADYGmEHAADYGmEHAADYGmEHAADYGmEHAADYGmEHAADYGmEHAADYGmEHAADYGmEHwC3r4MGDcjgcKigosLoUAD6MsAMAAGyNsAMAAGyNsAPA5124cEGzZ89W06ZN5XQ61ahRo8t+IWJVVZVGjx6txo0bKzg4WC1atNBLL73kNSY3N1f33Xef6tatq3r16ulHP/qRvvzyS0nSJ598oi5duigsLEzh4eFKTk7Wzp07b8ocAdQef6sLAIDvM23aNC1ZskQLFizQAw88oKKiIv3rX/+6ZNyFCxfUsGFDvf7664qOjta2bdv085//XG63W0OGDNH58+c1YMAAjR07Vn/6059UWVmpf/7zn3I4HJKkYcOG6d5779WiRYvk5+engoKC6/pmdAC+iW89B+DTTp48qQYNGmjhwoUaM2aMV9/BgwfVuHFjffzxx7rnnnsue/zjjz+ur776Sm+88YaOHz+uqKgo5ebmqlOnTpeMDQ8P1yuvvKIRI0bUxlQAWITLWAB82t69e+XxeNStW7drGv/73/9ebdu2VYMGDRQaGqolS5bo0KFDkqTIyEiNHDlSPXv2VN++ffXSSy+pqKjIPHbSpEkaM2aMUlNT9cILL+iLL76olTkBuLkIOwB8WnBw8DWPff311/WrX/1Ko0aN0saNG1VQUKCf/exnqqysNMdkZWXpo48+UocOHbR27Vo1b95c27dvlyRlZGRo9+7d6t27t7Zs2aJWrVopOzu7xucE4ObiMhYAn3b27FlFRkbq5Zdf/t7LWBMnTtSePXu0efNmc0xqaqq+/vrrKz6LJyUlRe3atdPLL798Sd8jjzyi06dPa926dTU6JwA3Fys7AHxaUFCQnnzySU2dOlUrVqzQF198oe3bt2vp0qWXjG3atKl27typ999/X/v379f06dO1Y8cOs7+wsFDTpk3TRx99pC+//FIbN27U/v371bJlS1VUVGjChAnKzc3Vl19+qQ8//FA7duxQy5Ytb+Z0AdQCPo0FwOdNnz5d/v7+mjFjho4ePSq3263HHnvsknGPPfaYCgoKNHToUDkcDj3yyCMaP3683nvvPUlSSEiI/vWvf2n58uU6duyY3G63JkyYoHHjxun8+fM6duyYhg8frq+++krR0dEaOHCgZs6cebOnC6CGcRkLAADYGpexAACArRF2AACArRF2AACArRF2AACArRF2AACArRF2AACArRF2AACArRF2AACArRF2AACArRF2AACArRF2AACArf1/xZ1tb8lt24IAAAAASUVORK5CYII="/>


```python
# class를 y 파라미터로 변경하여
# '선실 등급별 생존 여부를 나타내는 막대 그래프'를 만들어라

sns.countplot(data = df, y = 'class', hue = 'alive')
```

<pre>
<Axes: xlabel='count', ylabel='class'>
</pre>
<img src="data:image/png;base64,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0+rVq1WjRg116NBBXbt2VYMGDbR8+XKnjot3+QEA4GYq+yeXb968udCy1atXO36OiorSP//5z4obUDFwhgoAAMAQQQUAAGCIoAIAADBEUAEAABgiqAAAAAwRVAAAAIYIKgAAAEMEFQAAgCGCCgAAwBBBBQAAYIivngEAwM2kP397hf6+qMnJFfr7nMGtzlB16tRJY8aMcfYwAACAi3HJoEpMTJTNZit0mzlzpl544QWjfV/7lmsAAFD2Fi9erJCQEOXk5BRYPmDAAA0b9vOXOn/00Udq06aNfHx81KBBA02bNk1Xr151bDt16lRFRUXJbrcrIiJCTzzxRLmP2yWDSpJ69uypjIyMArc2bdooICCgyMfk5uZW4AgBAMCvDRw4UHl5eVqzZo1j2alTp/Txxx/roYce0ieffKLf/e53euKJJ3Tw4EHNmzdPixYt0ksvvSRJ+uCDDzR79mzNmzdPhw8f1urVq3X77eX/EqfLBpXdbldYWFiBW5cuXQq85Fe/fn29+OKLSkxMVFBQkEaOHKnc3FyNHj1a4eHh8vHxUf369TV9+nTH9pJ0//33y2azOe4DAICy4evrqwcffFALFy50LHv33XdVt25dderUSS+99JKeeeYZDR8+XA0aNFC3bt30wgsvaN68eZKk9PR0hYWFqWvXroqKilK7du00cuTIch+321+UPmvWLE2aNEnPPfecJOn111/XmjVr9P777ysqKkrHjx/X8ePHJUk7d+5UaGioFi5cqJ49e6patWrX3WdOTk6BU5XZ2dnlPxEAAFzEyJEj1bZtW33//fe65ZZbtHDhQsflPLt379bOnTsdZ6QkKS8vT5cvX9bFixc1cOBA/fWvf1WDBg3Us2dP3Xvvverbt688Pcs3eVw2qD7++GP5+/s77vfq1eu628XHx+upp55y3E9PT1ejRo10zz33yGazqV69eo51tWvXliQFBwcrLCysyN89ffp0TZs2rdDyd/1fU4DP9SMMzpH+/CxnD6HScod35QConO644w61bNlSixcvVo8ePZScnKyPPvpIkpSfn69p06apf//+hR7n4+OjyMhIHTp0SElJSdqwYYNGjRqlWbNmacuWLfLy8iq3MbtsUHXu3Fl///vfHferV6+uIUOGFNouNja2wP3ExER169ZNt912m3r27Kk+ffqoe/fuJfrdEyZM0NixYx33s7Oz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lOoM1YwZMzRv3jx16tRJQ4YMUcuWLSVJa9ascbwUeDNnz57Vtm3bNGPGDHXu3Fn16tVTu3btNGHCBMfnWmVlZemRRx5RaGioAgMDFR8fr6+++qrAftasWaPY2Fj5+PioVq1a6t+/v2PdTz/9pGHDhqlGjRry8/NTr169dPjwYcf6RYsWKTg4WJ988omaNm0qf39/9ezZs8BZtry8PI0dO1bBwcEKCQnR+PHjZVlWaZ42AADgokoVVJ06ddKpU6d06tQpvf32247ljzzyiObOnVusffj7+8vf31+rV69WTk5OofWWZal37946efKk1q1bp927d6t169bq0qWL4wzW2rVr1b9/f/Xu3Vt79+7Vxo0bFRsb69hHYmKidu3apTVr1uiLL76QZVm69957deXKFcc2Fy9e1F/+8hctWbJEW7duVXp6up566inH+ldeeUVvv/22FixYoG3btunMmTNatWrVDeeWk5Oj7OzsAjcAAOC6bJYTT7esXLlSI0eO1KVLl9S6dWt17NhRgwcPVkxMjD799FPdf//9yszMdFyvJUkNGzbU+PHj9cgjj6h9+/Zq0KCB/vGPfxTa9+HDh9W4cWN9/vnnjg8bPX36tCIjI/XOO+9o4MCBWrRokR566CEdOXJEt956qyTpjTfe0PPPP6+TJ09KkiIiIvTkk0/q6aefliRdvXpV0dHRatOmjVavXn3deU2dOlXTpk0rtPzAhKYK8OFzuqqaqMmFP3MNAOD6srOzFRQUpKysLAUGBt5w21JdQyX9/Kno77//vtLT05Wbm1tg3Z49e4q1jwEDBqh379767LPP9MUXX2j9+vWaOXOm3nrrLf344486f/58oWuyLl26pKNHj0qS9u3bp5EjR1533ykpKfL09NSdd97pWBYSEqLbbrtNKSkpjmV+fn6OmJKk8PBwZWZmSvr5JceMjAzFxcU51nt6eio2NvaGL/tNmDBBY8eOddzPzs5WZGRkcZ4SAABQBZXqJb/XX39dDz30kEJDQ7V37161a9dOISEhOnbsmHr16lWiffn4+Khbt26aPHmytm/frsTERE2ZMkX5+fkKDw/Xvn37CtwOHTqkP/3pT5IkX1/fIvdbVPBYliWbzea4/+sPIrXZbMbXSNntdgUGBha4AQAA11WqoHrjjTf05ptvas6cOfL29tb48eOVlJSkJ554QllZWUYDatas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"/>

#### 함수 사용법 궁금할 때 : Help 함수 활용(68쪽)



```python
# sns.countplot() 매뉴얼 출력

sns.countplot?
```
```
Signature:
sns.countplot(
    data=None,
    *,
    x=None,
    y=None,
    hue=None,
    order=None,
    hue_order=None,
    orient=None,
    color=None,
    palette=None,
    saturation=0.75,
    width=0.8,
    dodge=True,
    ax=None,
    **kwargs,

Show the counts of observations in each categorical bin using bars.

A count plot can be thought of as a histogram across a categorical, instead
of quantitative, variable. The basic API and options are identical to those
for :func:`barplot`, so you can compare counts across nested variables.

Note that the newer :func:`histplot` function offers more functionality, although
its default behavior is somewhat different.

.. note::
    This function always treats one of the variables as categorical and
    draws data at ordinal positions (0, 1, ... n) on the relevant axis,
    even when the data has a numeric or date type.

See the :ref:`tutorial <categorical_tutorial>` for more information.    

Parameters
----------
data : DataFrame, array, or list of arrays, optional
    Dataset for plotting. If ``x`` and ``y`` are absent, this is
    interpreted as wide-form. Otherwise it is expected to be long-form.    
x, y, hue : names of variables in ``data`` or vector data, optional
    Inputs for plotting long-form data. See examples for interpretation.    
order, hue_order : lists of strings, optional
    Order to plot the categorical levels in; otherwise the levels are
    inferred from the data objects.    
orient : "v" | "h", optional
    Orientation of the plot (vertical or horizontal). This is usually
    inferred based on the type of the input variables, but it can be used
    to resolve ambiguity when both `x` and `y` are numeric or when
    plotting wide-form data.    
color : matplotlib color, optional
    Single color for the elements in the plot.    
palette : palette name, list, or dict
    Colors to use for the different levels of the ``hue`` variable. Should
    be something that can be interpreted by :func:`color_palette`, or a
    dictionary mapping hue levels to matplotlib colors.    
saturation : float, optional
    Proportion of the original saturation to draw colors at. Large patches
    often look better with slightly desaturated colors, but set this to
    `1` if you want the plot colors to perfectly match the input color.    
dodge : bool, optional
    When hue nesting is used, whether elements should be shifted along the
    categorical axis.    
ax : matplotlib Axes, optional
    Axes object to draw the plot onto, otherwise uses the current Axes.    
kwargs : key, value mappings
    Other keyword arguments are passed through to
    :meth:`matplotlib.axes.Axes.bar`.

Returns
-------
ax : matplotlib Axes
    Returns the Axes object with the plot drawn onto it.    

See Also
--------
barplot : Show point estimates and confidence intervals using bars.    
catplot : Combine a categorical plot with a :class:`FacetGrid`.    

Examples
--------

.. include:: ../docstrings/countplot.rst
[1;31mFile:[0m      c:\users\creta\anaconda3\lib\site-packages\seaborn\categorical.py
[1;31mType:[0m      function
```

### 모듈 알아 보기(69쪽)



```python
# sklearn 패키지의 metrics 모듈 로드하기

import sklearn.metrics
```


```python
# sklearn 패키지 metrics 모듈의 accuracy_score() 함수 사용하기
                           # 일단 여기서는 함수에 값 입력하지 않아 에러 메시지 출력됨
sklearn.metrics.accuracy_score()
```

#### 모듈명.함수명()으로 함수 사용하기(70쪽)



```python
# sklearn 패키지의 metrics 모듈 로드하기
from sklearn import metrics
```


```python
# sklearn 패키지 metrics 모듈의 accuracy_score() 로드하기
metrics.accuracy_score()
```

### [Do it! 실습] 패키지 설치하기(71쪽)

- 아나콘다에 들어있지 <span style="color:red">않은</span> 패키지 사용할 때 직접 설치 필요

- PyDataset : 여러 가지 데이터 셋을 손쉽게 불러올 수 있음.


[용어/ChatGPT] 데이터셋

- 관련된 데이터의 모음.

- 일반적으로 표나 데이터베이스 형태로 구성되어 있으며, 여러 행과 열로 이루어져 있음.

- 각 행은 개별 기록이나 관측치를 나타내고, 각 열은 해당 데이터의 다양한 속성이나 변수를 나타냄.

- ex) 학교의 학생 정보를 담은 데이터셋

    - 각 학생(행)에 대한 정보가 포함

    - 학생의 이름, 나이, 성별, 성적 등(열)이 데이터로 기록됨



```python
pip install pydataset
```

<pre>
Requirement already satisfied: pydataset in c:\users\creta\anaconda3\lib\site-packages (0.2.0)
Requirement already satisfied: pandas in c:\users\creta\anaconda3\lib\site-packages (from pydataset) (2.0.3)
Requirement already satisfied: python-dateutil>=2.8.2 in c:\users\creta\anaconda3\lib\site-packages (from pandas->pydataset) (2.8.2)
Requirement already satisfied: pytz>=2020.1 in c:\users\creta\anaconda3\lib\site-packages (from pandas->pydataset) (2023.3.post1)
Requirement already satisfied: tzdata>=2022.1 in c:\users\creta\anaconda3\lib\site-packages (from pandas->pydataset) (2023.3)
Requirement already satisfied: numpy>=1.21.0 in c:\users\creta\anaconda3\lib\site-packages (from pandas->pydataset) (1.24.3)
Requirement already satisfied: six>=1.5 in c:\users\creta\anaconda3\lib\site-packages (from python-dateutil>=2.8.2->pandas->pydataset) (1.16.0)
Note: you may need to restart the kernel to use updated packages.
</pre>
#### 패키지 함수 사용하기(72쪽)



```python
import pydataset
```


```python
# pydataset 패키지에 들어 있는 데이터셋 목록 출력
pydataset.data()
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
      <th>dataset_id</th>
      <th>title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AirPassengers</td>
      <td>Monthly Airline Passenger Numbers 1949-1960</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BJsales</td>
      <td>Sales Data with Leading Indicator</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BOD</td>
      <td>Biochemical Oxygen Demand</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Formaldehyde</td>
      <td>Determination of Formaldehyde</td>
    </tr>
    <tr>
      <th>4</th>
      <td>HairEyeColor</td>
      <td>Hair and Eye Color of Statistics Students</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>752</th>
      <td>VerbAgg</td>
      <td>Verbal Aggression item responses</td>
    </tr>
    <tr>
      <th>753</th>
      <td>cake</td>
      <td>Breakage Angle of Chocolate Cakes</td>
    </tr>
    <tr>
      <th>754</th>
      <td>cbpp</td>
      <td>Contagious bovine pleuropneumonia</td>
    </tr>
    <tr>
      <th>755</th>
      <td>grouseticks</td>
      <td>Data on red grouse ticks from Elston et al. 2001</td>
    </tr>
    <tr>
      <th>756</th>
      <td>sleepstudy</td>
      <td>Reaction times in a sleep deprivation study</td>
    </tr>
  </tbody>
</table>
<p>757 rows × 2 columns</p>
</div>



```python
# data()에 'mtcars' 입력해 mtcars 데이터셋을 불러옴
## mtcars 데이터셋 : 자동자 32종의 정보 담고 있음

pydataset.data('mtcars')
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
      <th>mpg</th>
      <th>cyl</th>
      <th>disp</th>
      <th>hp</th>
      <th>drat</th>
      <th>wt</th>
      <th>qsec</th>
      <th>vs</th>
      <th>am</th>
      <th>gear</th>
      <th>carb</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mazda RX4</th>
      <td>21.0</td>
      <td>6</td>
      <td>160.0</td>
      <td>110</td>
      <td>3.90</td>
      <td>2.620</td>
      <td>16.46</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Mazda RX4 Wag</th>
      <td>21.0</td>
      <td>6</td>
      <td>160.0</td>
      <td>110</td>
      <td>3.90</td>
      <td>2.875</td>
      <td>17.02</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Datsun 710</th>
      <td>22.8</td>
      <td>4</td>
      <td>108.0</td>
      <td>93</td>
      <td>3.85</td>
      <td>2.320</td>
      <td>18.61</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Hornet 4 Drive</th>
      <td>21.4</td>
      <td>6</td>
      <td>258.0</td>
      <td>110</td>
      <td>3.08</td>
      <td>3.215</td>
      <td>19.44</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Hornet Sportabout</th>
      <td>18.7</td>
      <td>8</td>
      <td>360.0</td>
      <td>175</td>
      <td>3.15</td>
      <td>3.440</td>
      <td>17.02</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Valiant</th>
      <td>18.1</td>
      <td>6</td>
      <td>225.0</td>
      <td>105</td>
      <td>2.76</td>
      <td>3.460</td>
      <td>20.22</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Duster 360</th>
      <td>14.3</td>
      <td>8</td>
      <td>360.0</td>
      <td>245</td>
      <td>3.21</td>
      <td>3.570</td>
      <td>15.84</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Merc 240D</th>
      <td>24.4</td>
      <td>4</td>
      <td>146.7</td>
      <td>62</td>
      <td>3.69</td>
      <td>3.190</td>
      <td>20.00</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Merc 230</th>
      <td>22.8</td>
      <td>4</td>
      <td>140.8</td>
      <td>95</td>
      <td>3.92</td>
      <td>3.150</td>
      <td>22.90</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Merc 280</th>
      <td>19.2</td>
      <td>6</td>
      <td>167.6</td>
      <td>123</td>
      <td>3.92</td>
      <td>3.440</td>
      <td>18.30</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Merc 280C</th>
      <td>17.8</td>
      <td>6</td>
      <td>167.6</td>
      <td>123</td>
      <td>3.92</td>
      <td>3.440</td>
      <td>18.90</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Merc 450SE</th>
      <td>16.4</td>
      <td>8</td>
      <td>275.8</td>
      <td>180</td>
      <td>3.07</td>
      <td>4.070</td>
      <td>17.40</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Merc 450SL</th>
      <td>17.3</td>
      <td>8</td>
      <td>275.8</td>
      <td>180</td>
      <td>3.07</td>
      <td>3.730</td>
      <td>17.60</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Merc 450SLC</th>
      <td>15.2</td>
      <td>8</td>
      <td>275.8</td>
      <td>180</td>
      <td>3.07</td>
      <td>3.780</td>
      <td>18.00</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Cadillac Fleetwood</th>
      <td>10.4</td>
      <td>8</td>
      <td>472.0</td>
      <td>205</td>
      <td>2.93</td>
      <td>5.250</td>
      <td>17.98</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Lincoln Continental</th>
      <td>10.4</td>
      <td>8</td>
      <td>460.0</td>
      <td>215</td>
      <td>3.00</td>
      <td>5.424</td>
      <td>17.82</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Chrysler Imperial</th>
      <td>14.7</td>
      <td>8</td>
      <td>440.0</td>
      <td>230</td>
      <td>3.23</td>
      <td>5.345</td>
      <td>17.42</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Fiat 128</th>
      <td>32.4</td>
      <td>4</td>
      <td>78.7</td>
      <td>66</td>
      <td>4.08</td>
      <td>2.200</td>
      <td>19.47</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Honda Civic</th>
      <td>30.4</td>
      <td>4</td>
      <td>75.7</td>
      <td>52</td>
      <td>4.93</td>
      <td>1.615</td>
      <td>18.52</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Toyota Corolla</th>
      <td>33.9</td>
      <td>4</td>
      <td>71.1</td>
      <td>65</td>
      <td>4.22</td>
      <td>1.835</td>
      <td>19.90</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Toyota Corona</th>
      <td>21.5</td>
      <td>4</td>
      <td>120.1</td>
      <td>97</td>
      <td>3.70</td>
      <td>2.465</td>
      <td>20.01</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Dodge Challenger</th>
      <td>15.5</td>
      <td>8</td>
      <td>318.0</td>
      <td>150</td>
      <td>2.76</td>
      <td>3.520</td>
      <td>16.87</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>AMC Javelin</th>
      <td>15.2</td>
      <td>8</td>
      <td>304.0</td>
      <td>150</td>
      <td>3.15</td>
      <td>3.435</td>
      <td>17.30</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Camaro Z28</th>
      <td>13.3</td>
      <td>8</td>
      <td>350.0</td>
      <td>245</td>
      <td>3.73</td>
      <td>3.840</td>
      <td>15.41</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Pontiac Firebird</th>
      <td>19.2</td>
      <td>8</td>
      <td>400.0</td>
      <td>175</td>
      <td>3.08</td>
      <td>3.845</td>
      <td>17.05</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Fiat X1-9</th>
      <td>27.3</td>
      <td>4</td>
      <td>79.0</td>
      <td>66</td>
      <td>4.08</td>
      <td>1.935</td>
      <td>18.90</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Porsche 914-2</th>
      <td>26.0</td>
      <td>4</td>
      <td>120.3</td>
      <td>91</td>
      <td>4.43</td>
      <td>2.140</td>
      <td>16.70</td>
      <td>0</td>
      <td>1</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Lotus Europa</th>
      <td>30.4</td>
      <td>4</td>
      <td>95.1</td>
      <td>113</td>
      <td>3.77</td>
      <td>1.513</td>
      <td>16.90</td>
      <td>1</td>
      <td>1</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Ford Pantera L</th>
      <td>15.8</td>
      <td>8</td>
      <td>351.0</td>
      <td>264</td>
      <td>4.22</td>
      <td>3.170</td>
      <td>14.50</td>
      <td>0</td>
      <td>1</td>
      <td>5</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Ferrari Dino</th>
      <td>19.7</td>
      <td>6</td>
      <td>145.0</td>
      <td>175</td>
      <td>3.62</td>
      <td>2.770</td>
      <td>15.50</td>
      <td>0</td>
      <td>1</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Maserati Bora</th>
      <td>15.0</td>
      <td>8</td>
      <td>301.0</td>
      <td>335</td>
      <td>3.54</td>
      <td>3.570</td>
      <td>14.60</td>
      <td>0</td>
      <td>1</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Volvo 142E</th>
      <td>21.4</td>
      <td>4</td>
      <td>121.0</td>
      <td>109</td>
      <td>4.11</td>
      <td>2.780</td>
      <td>18.60</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>


### [개인 실습] 혼자서 해보기(73쪽)


#### Q1 : 시험 점수 변수 만들고 출력하기

- 학생 5명의 시험 점수를 담고 있는 변수 score 를 만들어 출력하시오. 학생들 시험 점수는 다음과 같습니다.  

- 80, 60, 70, 50, 90



```python
# A1
score = [80, 60, 70, 50, 90]
score
```

<pre>
[80, 60, 70, 50, 90]
</pre>
#### Q2 : 합계 점수 구하기

앞 문제에서 만든 변수를 이용해 합계 점수를 구해 보세요



```python
# A2
sum(score)
```

<pre>
350
</pre>
#### Q3 : 합계 점수를 변수 만들어 출력하기

- 합계 점수를 담고 있는 세 변수를 만들어 sum_score라는 변수에 담아 출력하시오. 

- 앞 문제 풀 때 사용한 코드를 응용하면 됨



```python
# A3
sum_score = sum(score)
sum_score
```

<pre>
350
</pre>
# <span style="color:blue; font-weight:bold;">The End of Note</span>

