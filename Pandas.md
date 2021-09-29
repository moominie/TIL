# Data Handling - Pandas

Pandas는 파이썬에서 데이터 핸들링을 가능하게 해주는 가장 인기 있는 라이브러리

Pandas의 핵심 객체는 DataFrame인데, DataFrame은 여러 개의 행과 열로 이루어진 2차원 데이터를 담는 데이터 구조체다.

Index는 RDBMS의 PK처럼 개별 데이터를 고유하게 식별하는 Key 값

Series는 칼럼이 하나뿐인 데이터 구조체, DataFrame은 칼럼이 여러 개인 데이터 구조체

## 파일을 DataFrame으로 로딩


```python
import pandas as pd
```

Kaggle에서 타이타닉 탑승자 데이터 파일 내려받기  
https://www.kaggle.com/c/titanic/data  
train.csv를 Jupyter Notebook의 디렉터리로 titanic_train.csv라는 파일명으로 변경해서 내려받기

- **pd.read_csv('[filepath/]파일명', [sep=','])**


```python
titanic_df = pd.read_csv('titanic_train.csv')
print('titanic 변수 type:', type(titanic_df))
titanic_df
```

    titanic 변수 type: <class 'pandas.core.frame.DataFrame'>





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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr....</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mr...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, ...</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 31...</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, M...</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. ...</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
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
      <th>886</th>
      <td>887</td>
      <td>0</td>
      <td>2</td>
      <td>Montvila, R...</td>
      <td>male</td>
      <td>27.0</td>
      <td>0</td>
      <td>0</td>
      <td>211536</td>
      <td>13.0000</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>887</th>
      <td>888</td>
      <td>1</td>
      <td>1</td>
      <td>Graham, Mis...</td>
      <td>female</td>
      <td>19.0</td>
      <td>0</td>
      <td>0</td>
      <td>112053</td>
      <td>30.0000</td>
      <td>B42</td>
      <td>S</td>
    </tr>
    <tr>
      <th>888</th>
      <td>889</td>
      <td>0</td>
      <td>3</td>
      <td>Johnston, M...</td>
      <td>female</td>
      <td>NaN</td>
      <td>1</td>
      <td>2</td>
      <td>W./C. 6607</td>
      <td>23.4500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>889</th>
      <td>890</td>
      <td>1</td>
      <td>1</td>
      <td>Behr, Mr. K...</td>
      <td>male</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>111369</td>
      <td>30.0000</td>
      <td>C148</td>
      <td>C</td>
    </tr>
    <tr>
      <th>890</th>
      <td>891</td>
      <td>0</td>
      <td>3</td>
      <td>Dooley, Mr....</td>
      <td>male</td>
      <td>32.0</td>
      <td>0</td>
      <td>0</td>
      <td>370376</td>
      <td>7.7500</td>
      <td>NaN</td>
      <td>Q</td>
    </tr>
  </tbody>
</table>
<p>891 rows × 12 columns</p>
</div>




- **DataFrame.head() : DataFrame의 맨 앞에 있는 N개의 로우 반환, default는 5개**


```python
titanic_df.head(3)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




- **DataFrame.shape : DataFrame의 행과 열을 튜플 형태로 반환**


```python
titanic_df.shape
```




    (891, 12)




```python
#titanic_df 객체는 891개의 로우와 12개의 칼럼으로 이루어짐
```


- **DataFrame.info() : 총 데이터 건수, 데이터 타입, Null 건수 알려주는 메서드**


```python
titanic_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 12 columns):
     #   Column       Non-Null Count  Dtype  
    ---  ------       --------------  -----  
     0   PassengerId  891 non-null    int64  
     1   Survived     891 non-null    int64  
     2   Pclass       891 non-null    int64  
     3   Name         891 non-null    object 
     4   Sex          891 non-null    object 
     5   Age          714 non-null    float64
     6   SibSp        891 non-null    int64  
     7   Parch        891 non-null    int64  
     8   Ticket       891 non-null    object 
     9   Fare         891 non-null    float64
     10  Cabin        204 non-null    object 
     11  Embarked     889 non-null    object 
    dtypes: float64(2), int64(5), object(5)
    memory usage: 83.7+ KB



- **DataFrame.describe() : 칼럼별 숫자형 데이터값의 Not Null인 데이터 건수, 평균값, 표준편차, 최솟값, 최댓값, n-percentile 분포도 등을 알려주는 메서드**  
describe() 메서드로 개략적인 수준의 데이터 분포도를 확인할 수 있음 -> 머신러닝 성능 향상시키는 중요한 요소!


```python
titanic_df.describe()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>714.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>446.000000</td>
      <td>0.383838</td>
      <td>2.308642</td>
      <td>29.699118</td>
      <td>0.523008</td>
      <td>0.381594</td>
      <td>32.204208</td>
    </tr>
    <tr>
      <th>std</th>
      <td>257.353842</td>
      <td>0.486592</td>
      <td>0.836071</td>
      <td>14.526497</td>
      <td>1.102743</td>
      <td>0.806057</td>
      <td>49.693429</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.420000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>223.500000</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>20.125000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>7.910400</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>446.000000</td>
      <td>0.000000</td>
      <td>3.000000</td>
      <td>28.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>14.454200</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>668.500000</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>38.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>31.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>891.000000</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>80.000000</td>
      <td>8.000000</td>
      <td>6.000000</td>
      <td>512.329200</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Survived 칼럼은 0과 1로 이루어진 숫자형 카테고리 칼럼, Pclass도 1, 2, 3으로 이루어진 숫자형 카테고리 칼럼
```


- **DataFrame['칼럼명'] : Series 형태로 특정 칼럼 데이터 세트가 반환됨**

- **Series.value_counts() : 해당 칼럼값의 유형과 건수를 반환, 데이터의 분포도를 확인하는 데 매우 유용한 함수**


```python
value_counts = titanic_df['Pclass'].value_counts()
print(value_counts)
```

    3    491
    1    216
    2    184
    Name: Pclass, dtype: int64



```python

```

## DataFrame과 list, dict, Numpy ndarray 상호 변환

### Numpy ndarray, list, dict를 DataFrame으로 변환하기

- **pd.DataFrame(data, columns)**  
data : ndarray, list, dict  
columns : 칼럼명 list (칼럼명을 지정하지 않으면 자동으로 칼럼명을 할당)  


```python
#1차원 데이터로 DataFrame 만들기
```


```python
import numpy as np

col_name1=['col1']
list1 = [1, 2, 3]
array1 = np.array(list1)
print('array1 shape: ', array1.shape)

#list를 이용해 DataFrame 생성
df_list1 = pd.DataFrame(list1, columns=col_name1)
print('1차원 리스트로 만든 DataFrame:\n', df_list1)

#Numpy ndarray를 이용해 DataFrame 생성
df_array1 = pd.DataFrame(array1, columns=col_name1)
print('1차원 ndarray로 만든 DataFrame:\n', df_array1)
```

    array1 shape:  (3,)
    1차원 리스트로 만든 DataFrame:
        col1
    0     1
    1     2
    2     3
    1차원 ndarray로 만든 DataFrame:
        col1
    0     1
    1     2
    2     3



```python
#2차원 데이터로 DataFrame 만들기
```


```python
list2 = [[1, 2, 3],
         [11, 12, 13]]
array2 = np.array(list2)
print('array2 shape: ', array2.shape)

#3개의 칼럼명이 필요함
col_name2 = ['col1', 'col2', 'col3']

df_list2 = pd.DataFrame(list2, columns=col_name2)
print('2차원 리스트로 만든 DataFrame:\n', df_list2)

df_array2 = pd.DataFrame(array2, columns=col_name2)
print('2차원 ndarray로 만든 DataFrame:\n', df_array2)
```

    array2 shape:  (2, 3)
    2차원 리스트로 만든 DataFrame:
        col1  col2  col3
    0     1     2     3
    1    11    12    13
    2차원 ndarray로 만든 DataFrame:
        col1  col2  col3
    0     1     2     3
    1    11    12    13



dictionary를 DataFrame으로 변환하기  
딕셔너리의 Key는 칼럼명, Value는 키에 해당하는 칼럼 데이터로 변환된다.  
Key는 문자열로, Value는 리스트(또는 ndarray) 형태로 딕셔너리를 구성하기


```python
dict = {'col1':[1, 11], 'col2':[2, 12], 'col3':[3, 13]}
df_dict = pd.DataFrame(dict)
print('딕셔너리로 만든 DataFrame:\n', df_dict)
```

    딕셔너리로 만든 DataFrame:
        col1  col2  col3
    0     1     2     3
    1    11    12    13



```python

```

### DataFrame을 Numpy ndarray, list, dict로 변환하기

- **DataFrame.values : DataFrame 객체를 ndarray로 변환**


```python
array3 = df_dict.values
print('df_dict.values 타입: ', type(array3), \
     'df_dict.values shape: ', array3.shape)
print(array3)
```

    df_dict.values 타입:  <class 'numpy.ndarray'> df_dict.values shape:  (2, 3)
    [[ 1  2  3]
     [11 12 13]]


- **DataFrame.values.tolist() : DataFrame을 ndarray로 변환하고 list로 최종 변환**


```python
list3 = df_dict.values.tolist()
print('df_dict.values.tolist() 타입: ', type(list3))
print(list3)
```

    df_dict.values.tolist() 타입:  <class 'list'>
    [[1, 2, 3], [11, 12, 13]]


- **DataFrame.to_dict() : DataFrame 객체를 딕셔너리로 변환**  
인자로 'list'를 입력하면 딕셔너리의 값이 리스트로 반환됨


```python
dict3 = df_dict.to_dict('list')
print('df_dict.to_dict() 타입: ', type(dict3))
print(dict3)
```

    df_dict.to_dict() 타입:  <class 'dict'>
    {'col1': [1, 11], 'col2': [2, 12], 'col3': [3, 13]}



```python

```

## DataFrame의 칼럼 데이터 세트 생성과 수정

- DataFrame['칼럼명']

DataFrame['칼럼명']=0과 같이 Series에 상숫값을 할당하면 Series의 모든 데이터 세트에 일괄적으로 적용됨


```python
#새로운 칼럼 Age_0을 추가하고 일괄적으로 0 값을 할당하기
```


```python
titanic_df['Age_0'] = 0
titanic_df.head(3)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Age_0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#기존 칼럼 Series를 가공해 새로운 칼럼 Series인 Age_by_10과 Family_No를 추가하기
```


```python
titanic_df['Age_by_10'] = titanic_df['Age']*10
titanic_df['Family_No'] = titanic_df['SibSp'] + titanic_df['Parch'] +1
titanic_df.head(3)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Age_0</th>
      <th>Age_by_10</th>
      <th>Family_No</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
      <td>0</td>
      <td>220.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
      <td>0</td>
      <td>380.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
      <td>0</td>
      <td>260.0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#기존 칼럼 'Age_by_10'값을 일괄적으로 기존 값 + 100으로 업데이트하기
```


```python
titanic_df['Age_by_10'] = titanic_df['Age_by_10'] + 100
titanic_df.head(3)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Age_0</th>
      <th>Age_by_10</th>
      <th>Family_No</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
      <td>0</td>
      <td>320.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
      <td>0</td>
      <td>480.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
      <td>0</td>
      <td>360.0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

## DataFrame 데이터 삭제

- **DataFrame.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors='raise')**  

가장 중요한 파라미터 : labels, axis, inplace  
**axis=0 : 로우 방향 축, axis=1 : 칼럼 방향 축**  
(예) drop('칼럼명', axis=1) : 지정된 칼럼을 드롭  
주로 칼럼을 드롭하므로 axis=1로 설정함  
(예) drop(index, axis=0) : 로우 레벨로 삭제, axis=0으로 설정하면 labels에 오는 값을 인덱스로 간주함, 이상치 데이터를 삭제하는 경우에 주로 사용 


```python
#Age_0 칼럼을 삭제
```


```python
titanic_drop_df = titanic_df.drop('Age_0', axis=1)
titanic_drop_df.head(3)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Age_by_10</th>
      <th>Family_No</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
      <td>320.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
      <td>480.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
      <td>360.0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
titanic_df.head(3) #원본 DataFrame 확인
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>Age_0</th>
      <th>Age_by_10</th>
      <th>Family_No</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
      <td>0</td>
      <td>320.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
      <td>0</td>
      <td>480.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
      <td>0</td>
      <td>360.0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




**inplace=False** : Default값, 원본 DataFrame의 데이터는 삭제하지 않으며, 삭제된 결과 DataFrame을 반환  

**inplace=True** : 원본 DataFrame의 데이터를 삭제하고 drop된 결과를 적용함, 단, 반환 값은 None이므로 반환 값을 다시 자신의 DataFrame 객체로 할당하면 안 됨!  

**labels** : 여러 개의 칼럼 삭제 시 삭제하고 싶은 칼럼명을 리스트 형태로 입력하고 labels 파라미터로 입력함


```python
#'Age_0', 'Age_by_10', 'Family_No' 3개의 칼럼 삭제하기
```


```python
drop_result = titanic_df.drop(['Age_0', 'Age_by_10', 'Family_No'], axis=1, inplace=True)
print('inplace=True로 drop 후 반환된 값: ', drop_result)
titanic_df.head(3)
```

    inplace=True로 drop 후 반환된 값:  None





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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
#axis=0으로 설정해 index 0, 1, 2(맨 앞 3개 데이터) 로우 삭제하기
```


```python
pd.set_option('display.width', 1000)
pd.set_option('display.max_colwidth', 15)
```


```python
print('###before axis 0 drop###')
print(titanic_df.head(3))

titanic_df.drop([0,1,2], axis=0, inplace=True) #axis 0 drop

print('### after axis 0 drop###')
print(titanic_df.head(3))
```

    ###before axis 0 drop###
       PassengerId  Survived  Pclass            Name     Sex   Age  SibSp  Parch          Ticket     Fare Cabin Embarked
    0            1         0       3  Braund, Mr....    male  22.0      1      0       A/5 21171   7.2500   NaN        S
    1            2         1       1  Cumings, Mr...  female  38.0      1      0        PC 17599  71.2833   C85        C
    2            3         1       3  Heikkinen, ...  female  26.0      0      0  STON/O2. 31...   7.9250   NaN        S
    ### after axis 0 drop###
       PassengerId  Survived  Pclass            Name     Sex   Age  SibSp  Parch  Ticket     Fare Cabin Embarked
    3            4         1       1  Futrelle, M...  female  35.0      1      0  113803  53.1000  C123        S
    4            5         0       3  Allen, Mr. ...    male  35.0      0      0  373450   8.0500   NaN        S
    5            6         0       3  Moran, Mr. ...    male   NaN      0      0  330877   8.4583   NaN        Q



```python

```

## Index 객체

- DataFrame.index : DataFrame의 index 객체만 추출
- Series.index : Series의 index 객체만 추출


```python
#원본 파일 다시 로딩
titanic_df = pd.read_csv('titanic_train.csv')

#index 객체 추출
indexes = titanic_df.index
print(indexes)

#index 객체를 실제 값 array로 변환
print('Index 객체 array값:\n', indexes.values)
```

    RangeIndex(start=0, stop=891, step=1)
    Index 객체 array값:
     [  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17
      18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35
      36  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53
      54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71
      72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89
      90  91  92  93  94  95  96  97  98  99 100 101 102 103 104 105 106 107
     108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125
     126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143
     144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161
     162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179
     180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197
     198 199 200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215
     216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233
     234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251
     252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269
     270 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287
     288 289 290 291 292 293 294 295 296 297 298 299 300 301 302 303 304 305
     306 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323
     324 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341
     342 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359
     360 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377
     378 379 380 381 382 383 384 385 386 387 388 389 390 391 392 393 394 395
     396 397 398 399 400 401 402 403 404 405 406 407 408 409 410 411 412 413
     414 415 416 417 418 419 420 421 422 423 424 425 426 427 428 429 430 431
     432 433 434 435 436 437 438 439 440 441 442 443 444 445 446 447 448 449
     450 451 452 453 454 455 456 457 458 459 460 461 462 463 464 465 466 467
     468 469 470 471 472 473 474 475 476 477 478 479 480 481 482 483 484 485
     486 487 488 489 490 491 492 493 494 495 496 497 498 499 500 501 502 503
     504 505 506 507 508 509 510 511 512 513 514 515 516 517 518 519 520 521
     522 523 524 525 526 527 528 529 530 531 532 533 534 535 536 537 538 539
     540 541 542 543 544 545 546 547 548 549 550 551 552 553 554 555 556 557
     558 559 560 561 562 563 564 565 566 567 568 569 570 571 572 573 574 575
     576 577 578 579 580 581 582 583 584 585 586 587 588 589 590 591 592 593
     594 595 596 597 598 599 600 601 602 603 604 605 606 607 608 609 610 611
     612 613 614 615 616 617 618 619 620 621 622 623 624 625 626 627 628 629
     630 631 632 633 634 635 636 637 638 639 640 641 642 643 644 645 646 647
     648 649 650 651 652 653 654 655 656 657 658 659 660 661 662 663 664 665
     666 667 668 669 670 671 672 673 674 675 676 677 678 679 680 681 682 683
     684 685 686 687 688 689 690 691 692 693 694 695 696 697 698 699 700 701
     702 703 704 705 706 707 708 709 710 711 712 713 714 715 716 717 718 719
     720 721 722 723 724 725 726 727 728 729 730 731 732 733 734 735 736 737
     738 739 740 741 742 743 744 745 746 747 748 749 750 751 752 753 754 755
     756 757 758 759 760 761 762 763 764 765 766 767 768 769 770 771 772 773
     774 775 776 777 778 779 780 781 782 783 784 785 786 787 788 789 790 791
     792 793 794 795 796 797 798 799 800 801 802 803 804 805 806 807 808 809
     810 811 812 813 814 815 816 817 818 819 820 821 822 823 824 825 826 827
     828 829 830 831 832 833 834 835 836 837 838 839 840 841 842 843 844 845
     846 847 848 849 850 851 852 853 854 855 856 857 858 859 860 861 862 863
     864 865 866 867 868 869 870 871 872 873 874 875 876 877 878 879 880 881
     882 883 884 885 886 887 888 889 890]



```python
print(type(indexes.values))
print(indexes.values.shape)
print(indexes[:5].values) #슬라이싱 가능
print(indexes.values[:5])
print(indexes[6]) #인덱싱 가능
#indexes[0]=5 에러 발생 : 한 번 만들어진 Index 객체는 함부로 변경할 수 없음
```

    <class 'numpy.ndarray'>
    (891,)
    [0 1 2 3 4]
    [0 1 2 3 4]
    6



```python
series_fair = titanic_df['Fare']
print('Fair Series max값: ', series_fair.max())
print('Fair Series sum값: ', series_fair.sum())
print('sum() Fair Series: ', sum(series_fair))
print('Fair Series + 3:\n', (series_fair+3).head(3))
#Series 객체에 연산 함수를 적용할 때 Index는 연산에서 제외됨
```

    Fair Series max값:  512.3292
    Fair Series sum값:  28693.9493
    sum() Fair Series:  28693.949299999967
    Fair Series + 3:
     0    10.2500
    1    74.2833
    2    10.9250
    Name: Fare, dtype: float64



```python
#Index는 오직 식별용으로만 사용됨
```

- DataFrame.reset_index() : 새롭게 인덱스를 연속 숫자형으로 할당함, 기존 인덱스는 'index'라는 새로운 칼럼 명으로 추가함
- Series.reset_index() : 기존 index가 칼럼으로 추가돼 칼럼이 2개가 되므로 Series가 아닌 DataFrame이 반환됨  
reset_index의 파라미터 중 drop=True로 설정하면 기존 인덱스는 새로운 칼럼으로 추가되지 않고 삭제(drop)됨


```python
titanic_reset_df = titanic_df.reset_index(inplace=False)
titanic_reset_df.head(3)
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
      <th>index</th>
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr....</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mr...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, ...</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 31...</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Pclass 칼럼 Series의 value_counts()수행 시 'Pclass' 고유 값이 식별자 인덱스 역할을 함, 이를 연속 숫자형 인덱스로 만들기
```


```python
print('###before reset_index###')
value_counts = titanic_df['Pclass'].value_counts()
print(value_counts)
print('value_counts 객체 변수 타입: ', type(value_counts))

new_value_counts = value_counts.reset_index(inplace=False)
print('###after reset_index###')
print(new_value_counts)
print('new_value_counts 객체 변수 타입: ', type(new_value_counts))
```

    ###before reset_index###
    3    491
    1    216
    2    184
    Name: Pclass, dtype: int64
    value_counts 객체 변수 타입:  <class 'pandas.core.series.Series'>
    ###after reset_index###
       index  Pclass
    0      3     491
    1      1     216
    2      2     184
    new_value_counts 객체 변수 타입:  <class 'pandas.core.frame.DataFrame'>



```python

```

## 데이터 셀렉션 및 필터링

### DataFrame의 [ ] 연산자

- **DataFrame 뒤에 있는 [ ]는 칼럼만 지정할 수 있는 '칼럼 지정 연산자'**


```python
print('단일 칼럼 데이터 추출:\n', titanic_df['Pclass'].head(3))
print('\n여러 칼럼 데이터 추출:\n', titanic_df[['Survived', 'Pclass']].head(3))
```

    단일 칼럼 데이터 추출:
     0    3
    1    1
    2    3
    Name: Pclass, dtype: int64
    
    여러 칼럼 데이터 추출:
        Survived  Pclass
    0         0       3
    1         1       1
    2         1       3


- **DataFrame[ ]안에 숫자 index는 KeyError 오류 발생**


```python
#titanic_df[0] : KeyError 오류 발생
```

- **DataFrame[ ] 안에 슬라이싱 표현 가능**  
단, 사용을 권장하지는 않음


```python
titanic_df[0:2]
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr....</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mr...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
  </tbody>
</table>
</div>



- **DataFrame[ ] 안에 불린 인덱싱 표현 가능**


```python
#Pclass 칼럼 값이 3인 데이터 3개 추출하기
```


```python
titanic_df[titanic_df['Pclass'] == 3].head(3)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr....</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, ...</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 31...</td>
      <td>7.925</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. ...</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.050</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

### DataFrame의 ix[ ] 연산자

ix[ ] 연산자는 칼럼 명칭(label) 기반 인덱싱과 칼럼 위치(position) 기반 인덱싱 기능을 모두 제공하면서 코드가 혼돈을 주거나 가독성이 떨어지면서 현재는 Pandas에서 사라지게(deprecated) 됨

### 명칭(label) 기반 인덱싱과 위치(position) 기반 인덱싱의 구분


```python
#간단히 DataFrame 생성
```


```python
import pandas as pd
```


```python
data = {'Name': ['Chulmin', 'Eunkyung', 'Jinwoong', 'Soobeom'],
        'Year': [2011, 2016, 2015, 2015],
        'Gender': ['Male', 'Female', 'Male', 'Male']
       }
data_df = pd.DataFrame(data, index=['one', 'two', 'three', 'four'])
data_df
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
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>Chulmin</td>
      <td>2011</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>two</th>
      <td>Eunkyung</td>
      <td>2016</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>three</th>
      <td>Jinwoong</td>
      <td>2015</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>four</th>
      <td>Soobeom</td>
      <td>2015</td>
      <td>Male</td>
    </tr>
  </tbody>
</table>
</div>




```python
#data_df를 reset_index()로 새로운 숫자형 인덱스를 생성
data_df_reset = data_df.reset_index()
data_df_reset = data_df_reset.rename(columns={'index':'old_index'})
data_df_reset
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
      <th>old_index</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>one</td>
      <td>Chulmin</td>
      <td>2011</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>1</th>
      <td>two</td>
      <td>Eunkyung</td>
      <td>2016</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>2</th>
      <td>three</td>
      <td>Jinwoong</td>
      <td>2015</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>3</th>
      <td>four</td>
      <td>Soobeom</td>
      <td>2015</td>
      <td>Male</td>
    </tr>
  </tbody>
</table>
</div>




```python
#인덱스 값에 1을 더해서 1부터 시작하는 새로운 인덱스값 생성
data_df_reset.index = data_df_reset.index + 1
data_df_reset
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
      <th>old_index</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>one</td>
      <td>Chulmin</td>
      <td>2011</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>2</th>
      <td>two</td>
      <td>Eunkyung</td>
      <td>2016</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>3</th>
      <td>three</td>
      <td>Jinwoong</td>
      <td>2015</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>4</th>
      <td>four</td>
      <td>Soobeom</td>
      <td>2015</td>
      <td>Male</td>
    </tr>
  </tbody>
</table>
</div>



### DataFrame iloc[ ] 연산자

- **iloc[ ]은 위치 기반 인덱싱만 허용**  
행과 열 값으로 integer 또는 integer 형의 슬라이싱, 팬시 리스트 값을 입력  
불린 인덱싱은 제공하지 않음


```python
#data_df에서 첫 번째 행, 첫 번째 열의 데이터 추출하기
```


```python
data_df.iloc[0,0]
```




    'Chulmin'




- iloc[ ]에 위치 인덱싱이 아닌 명칭을 입력하면 오류 발생


```python
#data_df.iloc[0, 'Name']
```

- iloc[ ]에 문자열 인덱스를 행 위치에 입력해도 오류 발생


```python
#data_df.iloc['one', 0]
```


```python
#data_df_reset에서 iloc[0,1] 적용하기
```


```python
data_df_reset.iloc[0,1] #첫 번째 행, 두 번째 열 위치에 있는 값을 반환함
```




    'Chulmin'




```python

```

### DataFrame loc[ ] 연산자

- **loc[ ]은 명칭 기반으로 데이터를 추출**  
행 위치에는 DataFrame index 값을, 열 위치에는 칼럼 명을 입력


```python
#인덱스 값이 'one'인 행의 칼럼 명이 'name'인 데이터 추출
```


```python
data_df.loc['one', 'Name']
```




    'Chulmin'




```python
#인덱스 값이 정수형인 경우
```


```python
data_df_reset.loc[1, 'Name']
```




    'Chulmin'




```python
#data_df.loc[0, 'Name']은 오류 발생 : 인덱스값이 0인 행이 없기 때문
```


- loc[시작 값:종료 값] 슬라이싱을 적용하면 시작 값 ~ 종료 값까지 포함하는 것을 의미  
명칭 기반 인덱싱의 특성 때문


```python
print('명칭 기반 loc slicing\n', data_df.loc['one':'two', 'Name'])
```

    명칭 기반 loc slicing
     one     Chulmin
    two    Eunkyung
    Name: Name, dtype: object



```python
print(data_df_reset.loc[1:2, 'Name']) #인덱스가 1,2인 2개의 데이터 반환
```

    1     Chulmin
    2    Eunkyung
    Name: Name, dtype: object


### 불린 인덱싱

불린 인덱싱으로 처음부터 가져올 조건을 입력하면 자동으로 원하는 값을 필터링함  
[ ], ix[ ], loc[ ]에서 지원


```python
#승객 중 나이(Age)가 60세 초과인 데이터 추출하기
```


```python
titanic_df = pd.read_csv('titanic_train.csv')
titanic_boolean = titanic_df[titanic_df['Age']>60]
print(type(titanic_boolean))
titanic_boolean      
```

    <class 'pandas.core.frame.DataFrame'>





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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33</th>
      <td>34</td>
      <td>0</td>
      <td>2</td>
      <td>Wheadon, Mr. Edward H</td>
      <td>male</td>
      <td>66.0</td>
      <td>0</td>
      <td>0</td>
      <td>C.A. 24579</td>
      <td>10.5000</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>54</th>
      <td>55</td>
      <td>0</td>
      <td>1</td>
      <td>Ostby, Mr. Engelhart Cornelius</td>
      <td>male</td>
      <td>65.0</td>
      <td>0</td>
      <td>1</td>
      <td>113509</td>
      <td>61.9792</td>
      <td>B30</td>
      <td>C</td>
    </tr>
    <tr>
      <th>96</th>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>Goldschmidt, Mr. George B</td>
      <td>male</td>
      <td>71.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17754</td>
      <td>34.6542</td>
      <td>A5</td>
      <td>C</td>
    </tr>
    <tr>
      <th>116</th>
      <td>117</td>
      <td>0</td>
      <td>3</td>
      <td>Connors, Mr. Patrick</td>
      <td>male</td>
      <td>70.5</td>
      <td>0</td>
      <td>0</td>
      <td>370369</td>
      <td>7.7500</td>
      <td>NaN</td>
      <td>Q</td>
    </tr>
    <tr>
      <th>170</th>
      <td>171</td>
      <td>0</td>
      <td>1</td>
      <td>Van der hoef, Mr. Wyckoff</td>
      <td>male</td>
      <td>61.0</td>
      <td>0</td>
      <td>0</td>
      <td>111240</td>
      <td>33.5000</td>
      <td>B19</td>
      <td>S</td>
    </tr>
    <tr>
      <th>252</th>
      <td>253</td>
      <td>0</td>
      <td>1</td>
      <td>Stead, Mr. William Thomas</td>
      <td>male</td>
      <td>62.0</td>
      <td>0</td>
      <td>0</td>
      <td>113514</td>
      <td>26.5500</td>
      <td>C87</td>
      <td>S</td>
    </tr>
    <tr>
      <th>275</th>
      <td>276</td>
      <td>1</td>
      <td>1</td>
      <td>Andrews, Miss. Kornelia Theodosia</td>
      <td>female</td>
      <td>63.0</td>
      <td>1</td>
      <td>0</td>
      <td>13502</td>
      <td>77.9583</td>
      <td>D7</td>
      <td>S</td>
    </tr>
    <tr>
      <th>280</th>
      <td>281</td>
      <td>0</td>
      <td>3</td>
      <td>Duane, Mr. Frank</td>
      <td>male</td>
      <td>65.0</td>
      <td>0</td>
      <td>0</td>
      <td>336439</td>
      <td>7.7500</td>
      <td>NaN</td>
      <td>Q</td>
    </tr>
    <tr>
      <th>326</th>
      <td>327</td>
      <td>0</td>
      <td>3</td>
      <td>Nysveen, Mr. Johan Hansen</td>
      <td>male</td>
      <td>61.0</td>
      <td>0</td>
      <td>0</td>
      <td>345364</td>
      <td>6.2375</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>438</th>
      <td>439</td>
      <td>0</td>
      <td>1</td>
      <td>Fortune, Mr. Mark</td>
      <td>male</td>
      <td>64.0</td>
      <td>1</td>
      <td>4</td>
      <td>19950</td>
      <td>263.0000</td>
      <td>C23 C25 C27</td>
      <td>S</td>
    </tr>
    <tr>
      <th>456</th>
      <td>457</td>
      <td>0</td>
      <td>1</td>
      <td>Millet, Mr. Francis Davis</td>
      <td>male</td>
      <td>65.0</td>
      <td>0</td>
      <td>0</td>
      <td>13509</td>
      <td>26.5500</td>
      <td>E38</td>
      <td>S</td>
    </tr>
    <tr>
      <th>483</th>
      <td>484</td>
      <td>1</td>
      <td>3</td>
      <td>Turkula, Mrs. (Hedwig)</td>
      <td>female</td>
      <td>63.0</td>
      <td>0</td>
      <td>0</td>
      <td>4134</td>
      <td>9.5875</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>493</th>
      <td>494</td>
      <td>0</td>
      <td>1</td>
      <td>Artagaveytia, Mr. Ramon</td>
      <td>male</td>
      <td>71.0</td>
      <td>0</td>
      <td>0</td>
      <td>PC 17609</td>
      <td>49.5042</td>
      <td>NaN</td>
      <td>C</td>
    </tr>
    <tr>
      <th>545</th>
      <td>546</td>
      <td>0</td>
      <td>1</td>
      <td>Nicholson, Mr. Arthur Ernest</td>
      <td>male</td>
      <td>64.0</td>
      <td>0</td>
      <td>0</td>
      <td>693</td>
      <td>26.0000</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>555</th>
      <td>556</td>
      <td>0</td>
      <td>1</td>
      <td>Wright, Mr. George</td>
      <td>male</td>
      <td>62.0</td>
      <td>0</td>
      <td>0</td>
      <td>113807</td>
      <td>26.5500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>570</th>
      <td>571</td>
      <td>1</td>
      <td>2</td>
      <td>Harris, Mr. George</td>
      <td>male</td>
      <td>62.0</td>
      <td>0</td>
      <td>0</td>
      <td>S.W./PP 752</td>
      <td>10.5000</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>625</th>
      <td>626</td>
      <td>0</td>
      <td>1</td>
      <td>Sutton, Mr. Frederick</td>
      <td>male</td>
      <td>61.0</td>
      <td>0</td>
      <td>0</td>
      <td>36963</td>
      <td>32.3208</td>
      <td>D50</td>
      <td>S</td>
    </tr>
    <tr>
      <th>630</th>
      <td>631</td>
      <td>1</td>
      <td>1</td>
      <td>Barkworth, Mr. Algernon Henry Wilson</td>
      <td>male</td>
      <td>80.0</td>
      <td>0</td>
      <td>0</td>
      <td>27042</td>
      <td>30.0000</td>
      <td>A23</td>
      <td>S</td>
    </tr>
    <tr>
      <th>672</th>
      <td>673</td>
      <td>0</td>
      <td>2</td>
      <td>Mitchell, Mr. Henry Michael</td>
      <td>male</td>
      <td>70.0</td>
      <td>0</td>
      <td>0</td>
      <td>C.A. 24580</td>
      <td>10.5000</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>745</th>
      <td>746</td>
      <td>0</td>
      <td>1</td>
      <td>Crosby, Capt. Edward Gifford</td>
      <td>male</td>
      <td>70.0</td>
      <td>1</td>
      <td>1</td>
      <td>WE/P 5735</td>
      <td>71.0000</td>
      <td>B22</td>
      <td>S</td>
    </tr>
    <tr>
      <th>829</th>
      <td>830</td>
      <td>1</td>
      <td>1</td>
      <td>Stone, Mrs. George Nelson (Martha Evelyn)</td>
      <td>female</td>
      <td>62.0</td>
      <td>0</td>
      <td>0</td>
      <td>113572</td>
      <td>80.0000</td>
      <td>B28</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>851</th>
      <td>852</td>
      <td>0</td>
      <td>3</td>
      <td>Svensson, Mr. Johan</td>
      <td>male</td>
      <td>74.0</td>
      <td>0</td>
      <td>0</td>
      <td>347060</td>
      <td>7.7750</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
#60세가 넘는 승객의 이름과 나이만 추출하기
```


```python
titanic_df[titanic_df['Age']>60][['Name', 'Age']]
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
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33</th>
      <td>Wheadon, Mr. Edward H</td>
      <td>66.0</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Ostby, Mr. Engelhart Cornelius</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>96</th>
      <td>Goldschmidt, Mr. George B</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Connors, Mr. Patrick</td>
      <td>70.5</td>
    </tr>
    <tr>
      <th>170</th>
      <td>Van der hoef, Mr. Wyckoff</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>252</th>
      <td>Stead, Mr. William Thomas</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>275</th>
      <td>Andrews, Miss. Kornelia Theodosia</td>
      <td>63.0</td>
    </tr>
    <tr>
      <th>280</th>
      <td>Duane, Mr. Frank</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>326</th>
      <td>Nysveen, Mr. Johan Hansen</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>438</th>
      <td>Fortune, Mr. Mark</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>456</th>
      <td>Millet, Mr. Francis Davis</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>483</th>
      <td>Turkula, Mrs. (Hedwig)</td>
      <td>63.0</td>
    </tr>
    <tr>
      <th>493</th>
      <td>Artagaveytia, Mr. Ramon</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>545</th>
      <td>Nicholson, Mr. Arthur Ernest</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>555</th>
      <td>Wright, Mr. George</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>570</th>
      <td>Harris, Mr. George</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>625</th>
      <td>Sutton, Mr. Frederick</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>630</th>
      <td>Barkworth, Mr. Algernon Henry Wilson</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>672</th>
      <td>Mitchell, Mr. Henry Michael</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>745</th>
      <td>Crosby, Capt. Edward Gifford</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>829</th>
      <td>Stone, Mrs. George Nelson (Martha Evelyn)</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>851</th>
      <td>Svensson, Mr. Johan</td>
      <td>74.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#loc을 이용해서 동일한 결과 출력하기
```


```python
titanic_df.loc[titanic_df['Age']>60, ['Name', 'Age']]
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
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33</th>
      <td>Wheadon, Mr. Edward H</td>
      <td>66.0</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Ostby, Mr. Engelhart Cornelius</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>96</th>
      <td>Goldschmidt, Mr. George B</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Connors, Mr. Patrick</td>
      <td>70.5</td>
    </tr>
    <tr>
      <th>170</th>
      <td>Van der hoef, Mr. Wyckoff</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>252</th>
      <td>Stead, Mr. William Thomas</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>275</th>
      <td>Andrews, Miss. Kornelia Theodosia</td>
      <td>63.0</td>
    </tr>
    <tr>
      <th>280</th>
      <td>Duane, Mr. Frank</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>326</th>
      <td>Nysveen, Mr. Johan Hansen</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>438</th>
      <td>Fortune, Mr. Mark</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>456</th>
      <td>Millet, Mr. Francis Davis</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>483</th>
      <td>Turkula, Mrs. (Hedwig)</td>
      <td>63.0</td>
    </tr>
    <tr>
      <th>493</th>
      <td>Artagaveytia, Mr. Ramon</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>545</th>
      <td>Nicholson, Mr. Arthur Ernest</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>555</th>
      <td>Wright, Mr. George</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>570</th>
      <td>Harris, Mr. George</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>625</th>
      <td>Sutton, Mr. Frederick</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>630</th>
      <td>Barkworth, Mr. Algernon Henry Wilson</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>672</th>
      <td>Mitchell, Mr. Henry Michael</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>745</th>
      <td>Crosby, Capt. Edward Gifford</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>829</th>
      <td>Stone, Mrs. George Nelson (Martha Evelyn)</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>851</th>
      <td>Svensson, Mr. Johan</td>
      <td>74.0</td>
    </tr>
  </tbody>
</table>
</div>




- 여러 개의 복합 조건을 결합해 적용하기 : 개별 조건은 ( )로 묶고, 복합 조건 연산자를 사용한다.
1. and 조건일 때는 &
2. or 조건일 때는 |
3. Not 조건일 때는 ~


```python
#나이가 60세를 넘고, 선실 등급이 1등급이며, 성별이 여성인 승객 추출하기
```


```python
titanic_df[(titanic_df['Age']>60)&(titanic_df['Pclass']==1)&(titanic_df['Sex']=='female')]
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>275</th>
      <td>276</td>
      <td>1</td>
      <td>1</td>
      <td>Andrews, Miss. Kornelia Theodosia</td>
      <td>female</td>
      <td>63.0</td>
      <td>1</td>
      <td>0</td>
      <td>13502</td>
      <td>77.9583</td>
      <td>D7</td>
      <td>S</td>
    </tr>
    <tr>
      <th>829</th>
      <td>830</td>
      <td>1</td>
      <td>1</td>
      <td>Stone, Mrs. George Nelson (Martha Evelyn)</td>
      <td>female</td>
      <td>62.0</td>
      <td>0</td>
      <td>0</td>
      <td>113572</td>
      <td>80.0000</td>
      <td>B28</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
#개별 조건을 변수에 할당하고 이들 변수를 결합해서 불린 인덱싱 수행하기
```


```python
cond1 = titanic_df['Age']>60
cond2 = titanic_df['Pclass']==1
cond3 = titanic_df['Sex']=='female'
titanic_df[cond1&cond2&cond3]
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>275</th>
      <td>276</td>
      <td>1</td>
      <td>1</td>
      <td>Andrews, Miss. Kornelia Theodosia</td>
      <td>female</td>
      <td>63.0</td>
      <td>1</td>
      <td>0</td>
      <td>13502</td>
      <td>77.9583</td>
      <td>D7</td>
      <td>S</td>
    </tr>
    <tr>
      <th>829</th>
      <td>830</td>
      <td>1</td>
      <td>1</td>
      <td>Stone, Mrs. George Nelson (Martha Evelyn)</td>
      <td>female</td>
      <td>62.0</td>
      <td>0</td>
      <td>0</td>
      <td>113572</td>
      <td>80.0000</td>
      <td>B28</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

## 정렬, Aggregation 함수, GroupBy 적용

### DataFrame, Series의 정렬 - sort_values()

- sort_values()는 RDBMS SQL의 order by 키워드와 매우 유사함  
주요 입력 파라미터 : by, ascending, inplace  
by=['칼럼명'] : 해당 칼럼으로 정렬 수행, 여러 개의 칼럼으로 정렬하려면 리스트 형식으로 정렬하려는 칼럼명을 입력  
ascending=True : Default값, 오름차순 정렬  
ascending=False : 내림차순 정렬  
inplace=False : Default값, sort_values()를 호출한 DataFrame은 그대로 유지하며 정렬된 DataFrame을 반환  
inplace=True : 호출한 DataFrame의 정렬 결과를 그대로 적용함


```python
#Name 칼럼으로 오름차순 정렬해 반환
```


```python
titanic_sorted = titanic_df.sort_values(by=['Name'])
titanic_sorted.head(3)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>845</th>
      <td>846</td>
      <td>0</td>
      <td>3</td>
      <td>Abbing, Mr. Anthony</td>
      <td>male</td>
      <td>42.0</td>
      <td>0</td>
      <td>0</td>
      <td>C.A. 5547</td>
      <td>7.55</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>746</th>
      <td>747</td>
      <td>0</td>
      <td>3</td>
      <td>Abbott, Mr. Rossmore Edward</td>
      <td>male</td>
      <td>16.0</td>
      <td>1</td>
      <td>1</td>
      <td>C.A. 2673</td>
      <td>20.25</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>279</th>
      <td>280</td>
      <td>1</td>
      <td>3</td>
      <td>Abbott, Mrs. Stanton (Rosa Hunt)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>1</td>
      <td>C.A. 2673</td>
      <td>20.25</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Pclass, Name 칼럼으로 내림차순 정렬한 결과를 반환
```


```python
titanic_sorted = titanic_df.sort_values(by=['Pclass', 'Name'], ascending=False)
titanic_sorted.head(3)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>868</th>
      <td>869</td>
      <td>0</td>
      <td>3</td>
      <td>van Melkebeke, Mr. Philemon</td>
      <td>male</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>345777</td>
      <td>9.5</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>153</th>
      <td>154</td>
      <td>0</td>
      <td>3</td>
      <td>van Billiard, Mr. Austin Blyler</td>
      <td>male</td>
      <td>40.5</td>
      <td>0</td>
      <td>2</td>
      <td>A/5. 851</td>
      <td>14.5</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>282</th>
      <td>283</td>
      <td>0</td>
      <td>3</td>
      <td>de Pelsmaeker, Mr. Alfons</td>
      <td>male</td>
      <td>16.0</td>
      <td>0</td>
      <td>0</td>
      <td>345778</td>
      <td>9.5</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



### Aggregation 함수 적용

DataFrame에서 min(), max(), sum(), count()와 같은 aggregation 함수를 호출하면 모든 칼럼에 해당 aggregation을 적용한다.


```python
titanic_df.count()
```




    PassengerId    891
    Survived       891
    Pclass         891
    Name           891
    Sex            891
    Age            714
    SibSp          891
    Parch          891
    Ticket         891
    Fare           891
    Cabin          204
    Embarked       889
    dtype: int64




특정 칼럼에 aggregation 함수를 적용하기 위해서는 DataFrame에 대상 칼럼들만 추출해서 적용한다.


```python
titanic_df[['Age', 'Fare']].mean()
```




    Age     29.699118
    Fare    32.204208
    dtype: float64



### groupby( ) 적용

DataFrame의 groupby( ) 사용 시 입력 파라미터 by에 칼럼을 입력하면 대상 칼럼으로 groupby된다.  
이때, DataFrameGroupBy라는 또 다른 형태의 DataFrame을 반환한다.


```python
#Pclass 칼럼 기준으로 GroupBy된 DataFrameGroupBy 객체 반환하기
```


```python
titanic_groupby = titanic_df.groupby(by='Pclass')
print(type(titanic_groupby))
```

    <class 'pandas.core.groupby.generic.DataFrameGroupBy'>



DataFrame의 groupby()에 aggregation 함수를 호출하면 groupby() 대상 칼럼을 제외한 모든 칼럼에 해당 aggregation 함수를 적용한다.


```python
titanic_groupby = titanic_df.groupby('Pclass').count()
titanic_groupby
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
    <tr>
      <th>Pclass</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>216</td>
      <td>216</td>
      <td>216</td>
      <td>216</td>
      <td>186</td>
      <td>216</td>
      <td>216</td>
      <td>216</td>
      <td>216</td>
      <td>176</td>
      <td>214</td>
    </tr>
    <tr>
      <th>2</th>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>173</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>16</td>
      <td>184</td>
    </tr>
    <tr>
      <th>3</th>
      <td>491</td>
      <td>491</td>
      <td>491</td>
      <td>491</td>
      <td>355</td>
      <td>491</td>
      <td>491</td>
      <td>491</td>
      <td>491</td>
      <td>12</td>
      <td>491</td>
    </tr>
  </tbody>
</table>
</div>




DataFrame의 groupby()에 특정 칼럼만 aggregation 함수를 적용하려면 groupby()로 반환된 객체에 해당 칼럼을 필터링한 뒤 aggregation 함수를 적용한다.


```python
#Pclass로 groupby()하고, PassengerId, Survived 칼럼에만 count() 수행하기
```


```python
titanic_groupby = titanic_df.groupby('Pclass')[['PassengerId', 'Survived']].count()
titanic_groupby
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
      <th>PassengerId</th>
      <th>Survived</th>
    </tr>
    <tr>
      <th>Pclass</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>216</td>
      <td>216</td>
    </tr>
    <tr>
      <th>2</th>
      <td>184</td>
      <td>184</td>
    </tr>
    <tr>
      <th>3</th>
      <td>491</td>
      <td>491</td>
    </tr>
  </tbody>
</table>
</div>




DataFrame의 groupby()에 서로 다른 aggregation 함수를 적용할 경우에는 DataFrameGroupBy 객체의 agg( ) 내에 인자로 입력해서 사용한다.


```python
titanic_df.groupby('Pclass')['Age'].agg([max, min])
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
      <th>max</th>
      <th>min</th>
    </tr>
    <tr>
      <th>Pclass</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>80.0</td>
      <td>0.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>70.0</td>
      <td>0.67</td>
    </tr>
    <tr>
      <th>3</th>
      <td>74.0</td>
      <td>0.42</td>
    </tr>
  </tbody>
</table>
</div>




여러 개의 칼럼이 서로 다른 aggregation 함수를 groupby에서 호출하려면 agg( ) 내에 입력 값으로 딕셔너리 형태 {'aggregation이 적용될 칼럼': 'aggregation 함수'}를 입력한다.


```python
agg_format = {'Age':'max', 'SibSp':'sum', 'Fare':'mean'}
titanic_df.groupby('Pclass').agg(agg_format)
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
      <th>Age</th>
      <th>SibSp</th>
      <th>Fare</th>
    </tr>
    <tr>
      <th>Pclass</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>80.0</td>
      <td>90</td>
      <td>84.154687</td>
    </tr>
    <tr>
      <th>2</th>
      <td>70.0</td>
      <td>74</td>
      <td>20.662183</td>
    </tr>
    <tr>
      <th>3</th>
      <td>74.0</td>
      <td>302</td>
      <td>13.675550</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

## 결손 데이터 처리하기

- 결손 데이터 : 칼럼에 값이 없는(Null)인 경우를 의미하며, 이를 넘파이의 **NaN**으로 표시한다.  
기본적으로 Machine Learning은 NaN 값을 처리하지 않고, 평균, 총합 등의 함수 연산에서도 제외되므로 이 Nan 값을 다른 값으로 대체해야 한다.  
- **isna( ) : NaN 여부를 확인하는 API**  
- **fillna( ) : NaN 값을 다른 값으로 대체하는 API**

### isna( )로 결손 데이터 여부 확인

- isna( )는 데이터가 NaN인지 아닌지를 알려준다.  

DataFrame에 isna() 수행 시 모든 칼럼의 값에 대한 NaN 여부를 True, False로 알려준다.


```python
titanic_df.isna().head(3)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#isna() 결과에 sum() 함수를 추가해서 결손 데이터의 개수 구하기
```


```python
titanic_df.isna().sum()
```




    PassengerId      0
    Survived         0
    Pclass           0
    Name             0
    Sex              0
    Age            177
    SibSp            0
    Parch            0
    Ticket           0
    Fare             0
    Cabin          687
    Embarked         2
    dtype: int64



### fillna( )로 결손 데이터 대체하기

- fillna( )로 결손 데이터(NaN)를 다른 값으로 대체할 수 있다.
- **fillna()를 이용해 반환 값을 다시 받거나, inplace=True 파라미터를 추가해야 실제 데이터 세트 값이 변경된다.**


```python
#'Cabin' 칼럼의 NaN값을 'C000'으로 대체하기
```


```python
titanic_df['Cabin'] = titanic_df['Cabin'].fillna('C000') #fillna() 반환 값을 다시 받기
#titanic_df['Cabin'].fillna('C000', inplace=True)
titanic_df.head(3)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>C000</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>C000</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
#'Age' 칼럼의 NaN 값을 평균 나이로, 'Embarked' 칼럼의 NaN값을 'S'로 대체해 모든 결손 데이터를 처리하기
```


```python
titanic_df['Age'] = titanic_df['Age'].fillna(titanic_df['Age'].mean())
titanic_df['Embarked'] = titanic_df['Embarked'].fillna('S')
titanic_df.isna().sum()
```




    PassengerId    0
    Survived       0
    Pclass         0
    Name           0
    Sex            0
    Age            0
    SibSp          0
    Parch          0
    Ticket         0
    Fare           0
    Cabin          0
    Embarked       0
    dtype: int64




```python

```

## apply lambda 식으로 데이터 가공

복잡한 데이터의 가공이 필요한 경우 apply lambda를 이용한다.

- **lambda식**  
lambda 입력 인자 : 입력 인자의 계산식  
':'로 입력 인자와 반환될 입력 인자의 계산식을 분리한다.  
(예시) lambda x : x ** 2  


```python
def get_square(a):
    return a ** 2

print('3의 제곱은: ', get_square(3))
```

    3의 제곱은:  9



```python
lambda_square = lambda x : x ** 2
print('3의 제곱은: ', lambda_square(3))
```

    3의 제곱은:  9


- 여러 개의 값을 입력 인자로 사용해야 할 경우에는 map( ) 함수를 결합해서 사용한다.


```python
a = [1, 2, 3]
squares = map(lambda x : x ** 2, a)
list(squares)
```




    [1, 4, 9]



- DataFrame의 lambda식은 파이썬의 lambda식을 그대로 적용한 것  
- DataFrame.apply(lambda식)


```python
#'Name' 칼럼의 문자열 개수를 별도의 칼럼인 'Name_len'에 생성하기
```


```python
titanic_df['Name_len'] = titanic_df['Name'].apply(lambda x : len(x))
titanic_df[['Name', 'Name_len']].head(3)
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
      <th>Name</th>
      <th>Name_len</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Braund, Mr. Owen Harris</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>51</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Heikkinen, Miss. Laina</td>
      <td>22</td>
    </tr>
  </tbody>
</table>
</div>




```python
#lambda식에서 if else 절을 사용해서 나이가 15세 이하면 'Child', 그렇지 않으면 'Adult'로 구분하기
```


```python
titanic_df['Child_Adult'] = titanic_df['Age'].apply(lambda x : 'Child' if x <= 15 else 'Adult')
titanic_df[['Age', 'Child_Adult']].head(10)
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
      <th>Age</th>
      <th>Child_Adult</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>22.000000</td>
      <td>Adult</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38.000000</td>
      <td>Adult</td>
    </tr>
    <tr>
      <th>2</th>
      <td>26.000000</td>
      <td>Adult</td>
    </tr>
    <tr>
      <th>3</th>
      <td>35.000000</td>
      <td>Adult</td>
    </tr>
    <tr>
      <th>4</th>
      <td>35.000000</td>
      <td>Adult</td>
    </tr>
    <tr>
      <th>5</th>
      <td>29.699118</td>
      <td>Adult</td>
    </tr>
    <tr>
      <th>6</th>
      <td>54.000000</td>
      <td>Adult</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2.000000</td>
      <td>Child</td>
    </tr>
    <tr>
      <th>8</th>
      <td>27.000000</td>
      <td>Adult</td>
    </tr>
    <tr>
      <th>9</th>
      <td>14.000000</td>
      <td>Child</td>
    </tr>
  </tbody>
</table>
</div>




lambda식에서는 elif를 지원하지 않는다.  
조건식을 여러 개 사용하는 경우 else절을 ( )로 내포해 ( ) 내에서 다시 if, else를 적용해 사용한다.


```python
#나이가 15세 이하이면 Child, 15 ~ 60세 사이는 Adult, 61세 이상은 Elderly로 분류하는 'Age_Cat' 칼럼 만들기
```


```python
titanic_df['Age_Cat'] = titanic_df['Age'].apply(lambda x : 'Child' if x <= 15 else('Adult' if x <= 60 else 'Elderly'))
titanic_df['Age_Cat'].value_counts()
```




    Adult      786
    Child       83
    Elderly     22
    Name: Age_Cat, dtype: int64




조건식이 많을 때에는 별도의 함수를 만든다.


```python
#5살 이하는 Baby, 12살 이하는 Child, 18살 이하는 Teenage, 25살 이하는 Student,
#35살 이하는 Young Adult, 60세 이하는 Adult, 그 이상은 Elderly로 분류하기
```


```python
def get_category(age):
    cat = ''
    if age <= 5: cat = 'Baby'
    elif age <= 12: cat = 'Child'
    elif age <= 25: cat = 'Student'
    elif age <= 35: cat = 'Young Adult'
    elif age <= 60: cat = 'Adult'
    else: 'Elderly'
    return cat

#lambda식에서 위에서 생성한 get_category()함수를 반환값으로 지정
#get_category()함수는 입력값으로 'Age' 칼럼 값을 받아서 해당하는 cat으로 반환함

titanic_df['Age_Cat'] = titanic_df['Age'].apply(lambda x : get_category(x))
titanic_df[['Age', 'Age_Cat']].head()
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
      <th>Age</th>
      <th>Age_Cat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>22.0</td>
      <td>Student</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38.0</td>
      <td>Adult</td>
    </tr>
    <tr>
      <th>2</th>
      <td>26.0</td>
      <td>Young Adult</td>
    </tr>
    <tr>
      <th>3</th>
      <td>35.0</td>
      <td>Young Adult</td>
    </tr>
    <tr>
      <th>4</th>
      <td>35.0</td>
      <td>Young Adult</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
