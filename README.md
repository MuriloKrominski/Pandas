# Pandas
<a href="https://colab.research.google.com/github/MuriloKrominski/Pandas/blob/main/pandas.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab 0"/></a><br>

<!DOCTYPE html>
<html>
<body>
<div align="center">
<h3>Enjoy</h3>
    
<h1>Pandas - Series & Dataframes</h1>

</div>
</body>
</html>


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import glob
import re
import math
```


```python
import warnings
warnings.filterwarnings("ignore")
```


```python
#UPLOAD AND UNRAR
from google.colab import files
uploaded = files.upload()
```



<input type="file" id="files-13b7eb5f-ac0b-436a-8a59-6d39dd02b4c9" name="files[]" multiple disabled
   style="border:none" />
<output id="result-13b7eb5f-ac0b-436a-8a59-6d39dd02b4c9">
 Upload widget is only available when the cell has been executed in the
 current browser session. Please rerun this cell to enable.
 </output>
 <script src="/nbextensions/google.colab/files.js"></script> 


    Saving Exemplos[1].rar to Exemplos[1].rar
    

https://github.com/MuriloKrominski/Pandas/blob/main/Exemplos.rar?raw=true


```python
!unrar x /content/Exemplos[1].rar "/content/"
```

    
    UNRAR 5.50 freeware      Copyright (c) 1993-2017 Alexander Roshal
    
    
    Extracting from /content/Exemplos[1].rar
    
    Creating    /content/Exemplo                                          OK
    Extracting  /content/Exemplo/02-01-2020.csv                              4  OK 
    Extracting  /content/Exemplo/02-02-2020.csv                              9  OK 
    Extracting  /content/Exemplo/02-03-2020.csv                             15  OK 
    Extracting  /content/Exemplo/02-04-2020.csv                             20  OK 
    Extracting  /content/Exemplo/02-05-2020.csv                             26  OK 
    Creating    /content/Exemplo2                                         OK
    Extracting  /content/Exemplo2/pokemon.csv                               98  OK 
    All OK
    

# Series

## Create Series


```python
# Create series from Nump Array
v = np.array([1,2,3,4,5,6,7])
s1 = pd.Series(v)
s1
```




    0    1
    1    2
    2    3
    3    4
    4    5
    5    6
    6    7
    dtype: int64




```python
#Datatype of Series
s1.dtype
```




    dtype('int64')




```python
# number of bytes allocated to each item
v.itemsize
```




    8




```python
# Number of bytes consumed by Series
s1.nbytes
```




    56




```python
# Shape of the Series
s1.shape
```




    (7,)




```python
# number of dimensions
s1.ndim
```




    1




```python
# Length of Series
len(s1)
```




    7




```python
s1.count()
```




    7




```python
s1.size
```




    7




```python
# Create series from List 
s0 = pd.Series([1,2,3],index = ['a','b','c'])
s0
```




    a    1
    b    2
    c    3
    dtype: int64




```python
# Modifying index in Series
s1.index = ['a' , 'b' , 'c' , 'd' , 'e' , 'f' , 'g']
s1
```




    a    1
    b    2
    c    3
    d    4
    e    5
    f    6
    g    7
    dtype: int64




```python
# Create Series using Random and Range function
v2 = np.random.random(10)
ind2 = np.arange(0,10)
s = pd.Series(v2,ind2)
v2 , ind2 , s
```




    (array([0.9630357 , 0.25435325, 0.40378629, 0.42216504, 0.09347347,
            0.54178343, 0.02720533, 0.37324151, 0.37756028, 0.21619533]),
     array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]),
     0    0.963036
     1    0.254353
     2    0.403786
     3    0.422165
     4    0.093473
     5    0.541783
     6    0.027205
     7    0.373242
     8    0.377560
     9    0.216195
     dtype: float64)




```python
# Creating Series from Dictionary
dict1 = {'a1' :10 , 'a2' :20 , 'a3':30 , 'a4':40}
s3 = pd.Series(dict1)
s3
```




    a1    10
    a2    20
    a3    30
    a4    40
    dtype: int64




```python
pd.Series(99, index=[0, 1, 2, 3, 4, 5]) 
```




    0    99
    1    99
    2    99
    3    99
    4    99
    5    99
    dtype: int64



## Slicing Series


```python
s
```




    0    0.963036
    1    0.254353
    2    0.403786
    3    0.422165
    4    0.093473
    5    0.541783
    6    0.027205
    7    0.373242
    8    0.377560
    9    0.216195
    dtype: float64




```python
# Return all elements of the series
s[:]
```




    0    0.963036
    1    0.254353
    2    0.403786
    3    0.422165
    4    0.093473
    5    0.541783
    6    0.027205
    7    0.373242
    8    0.377560
    9    0.216195
    dtype: float64




```python
# First three element of the Series
s[0:3]
```




    0    0.963036
    1    0.254353
    2    0.403786
    dtype: float64




```python
# Last element of the Series
s[-1:]
```




    9    0.216195
    dtype: float64




```python
# Fetch first 4 elements in a series
s[:4]
```




    0    0.963036
    1    0.254353
    2    0.403786
    3    0.422165
    dtype: float64




```python
# Return all elements of the series except last two elements.
s[:-2]
```




    0    0.963036
    1    0.254353
    2    0.403786
    3    0.422165
    4    0.093473
    5    0.541783
    6    0.027205
    7    0.373242
    dtype: float64




```python
# Return all elements of the series except last element.
s[:-1]
```




    0    0.963036
    1    0.254353
    2    0.403786
    3    0.422165
    4    0.093473
    5    0.541783
    6    0.027205
    7    0.373242
    8    0.377560
    dtype: float64




```python
# Return last two elements of the series
s[-2:]
```




    8    0.377560
    9    0.216195
    dtype: float64




```python
# # Return last element of the series
s[-1:]
```




    9    0.216195
    dtype: float64




```python
s[-3:-1]
```




    7    0.373242
    8    0.377560
    dtype: float64



## Append Series


```python
s2 = s1.copy()
s2
```




    a    1
    b    2
    c    3
    d    4
    e    5
    f    6
    g    7
    dtype: int64




```python
s3
```




    a1    10
    a2    20
    a3    30
    a4    40
    dtype: int64




```python
# Append S2 & S3 Series
s4 = s2.append(s3)
s4
```




    a      1
    b      2
    c      3
    d      4
    e      5
    f      6
    g      7
    a1    10
    a2    20
    a3    30
    a4    40
    dtype: int64




```python
# When "inplace=False" it will return a new copy of data with the operation performed
s4.drop('a4' , inplace=False)
```




    a      1
    b      2
    c      3
    d      4
    e      5
    f      6
    g      7
    a1    10
    a2    20
    a3    30
    dtype: int64




```python
s4
```




    a      1
    b      2
    c      3
    d      4
    e      5
    f      6
    g      7
    a1    10
    a2    20
    a3    30
    a4    40
    dtype: int64




```python
# When we use "inplace=True" it will affect the dataframe
s4.drop('a4', inplace=True)
s4
```




    a      1
    b      2
    c      3
    d      4
    e      5
    f      6
    g      7
    a1    10
    a2    20
    a3    30
    dtype: int64




```python
s4 = s4.append(pd.Series({'a4': 7}))
s4
```




    a      1
    b      2
    c      3
    d      4
    e      5
    f      6
    g      7
    a1    10
    a2    20
    a3    30
    a4     7
    dtype: int64



## Operation on Series


```python
v1 = np.array([10,20,30])
v2 = np.array([1,2,3])
s1 = pd.Series(v1) 
s2 = pd.Series(v2)
s1 , s2
```




    (0    10
     1    20
     2    30
     dtype: int64, 0    1
     1    2
     2    3
     dtype: int64)




```python
# Addition of two series
s1.add(s2)
```




    0    11
    1    22
    2    33
    dtype: int64




```python
# Subtraction of two series
s1.sub(s2)
```




    0     9
    1    18
    2    27
    dtype: int64




```python
# Subtraction of two series
s1.subtract(s2)
```




    0     9
    1    18
    2    27
    dtype: int64




```python
# Increment all numbers in a series by 9
s1.add(9)
```




    0    19
    1    29
    2    39
    dtype: int64




```python
# Multiplication of two series
s1.mul(s2)
```




    0    10
    1    40
    2    90
    dtype: int64




```python
# Multiplication of two series
s1.multiply(s2)
```




    0    10
    1    40
    2    90
    dtype: int64




```python
# Multiply each element by 1000
s1.multiply(1000)
```




    0    10000
    1    20000
    2    30000
    dtype: int64




```python
# Division
s1.divide(s2)
```




    0    10.0
    1    10.0
    2    10.0
    dtype: float64




```python
# Division
s1.div(s2)
```




    0    10.0
    1    10.0
    2    10.0
    dtype: float64




```python
# MAX number in a series
s1.max()
```




    30




```python
# Min number in a series
s1.min()
```




    10




```python
# Average
s1.mean()
```




    20.0




```python
# Median
s1.median()
```




    20.0




```python
# Standard Deviation
s1.std()
```




    10.0




```python
# Series comparison
s1.equals(s2)
```




    False




```python
s4 =s1
```


```python
# Series comparison
s1.equals(s4)
```




    True




```python
s5 = pd.Series([1,1,2,2,3,3], index=[0, 1, 2, 3, 4, 5])
s5
```




    0    1
    1    1
    2    2
    3    2
    4    3
    5    3
    dtype: int64




```python
s5.value_counts()
```




    3    2
    2    2
    1    2
    dtype: int64



# DataFrame

## Create DataFrame


```python
df = pd.DataFrame()
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
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
# Create Dataframe using List
lang = ['Java' , 'Python' , 'C' , 'C++']
df = pd.DataFrame(lang)
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
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Java</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Python</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C++</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Add column in the Dataframe
rating = [1,2,3,4]
df[1] = rating
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
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Java</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Python</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C++</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.columns = ['Language','Rating']
```


```python
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
      <th>Language</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Java</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Python</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C++</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create Dataframe from Dictionary

data = [{'a': 1, 'b': 2},{'a': 5, 'b': 10, 'c': 20}]

df2 = pd.DataFrame(data)
df3 = pd.DataFrame(data, index=['row1', 'row2'], columns=['a', 'b'])
df4 = pd.DataFrame(data, index=['row1', 'row2'], columns=['a', 'b' ,'c'])
df5 = pd.DataFrame(data, index=['row1', 'row2'], columns=['a', 'b' ,'c' , 'd'])
```


```python
df2
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
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>10</td>
      <td>20.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3
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
      <th>row1</th>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>row2</th>
      <td>5</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
df4
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
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>row1</th>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>row2</th>
      <td>5</td>
      <td>10</td>
      <td>20.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df5
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
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>row1</th>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>row2</th>
      <td>5</td>
      <td>10</td>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create Dataframe from Dictionary
df0 = pd.DataFrame({'ID' :[1,2,3,4] , 'Name' :['Murilo' , 'Krominski' , 'Ross' , 'John']})
df0
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
      <th>ID</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Ross</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create a DataFrame from Dictionary of Series
dict = {'A' : pd.Series([1, 2, 3],    index=['a', 'b', 'c']),
        'B' : pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])}

df1 = pd.DataFrame(dict)
df1
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



#### Dataframe of Random Numbers with Date Indices


```python
dates = pd.date_range(start='2020-01-20', end='2020-01-26')
dates
```




    DatetimeIndex(['2020-01-20', '2020-01-21', '2020-01-22', '2020-01-23',
                   '2020-01-24', '2020-01-25', '2020-01-26'],
                  dtype='datetime64[ns]', freq='D')




```python
dates = pd.date_range('today',periods= 7)
dates
```




    DatetimeIndex(['2020-12-15 19:15:48.500699', '2020-12-16 19:15:48.500699',
                   '2020-12-17 19:15:48.500699', '2020-12-18 19:15:48.500699',
                   '2020-12-19 19:15:48.500699', '2020-12-20 19:15:48.500699',
                   '2020-12-21 19:15:48.500699'],
                  dtype='datetime64[ns]', freq='D')




```python
dates = pd.date_range(start='2020-01-20', periods=7)
dates
```




    DatetimeIndex(['2020-01-20', '2020-01-21', '2020-01-22', '2020-01-23',
                   '2020-01-24', '2020-01-25', '2020-01-26'],
                  dtype='datetime64[ns]', freq='D')




```python
M = np.random.random((7,7))
M
```




    array([[0.77053241, 0.1360533 , 0.83582236, 0.68993394, 0.36209114,
            0.06728942, 0.41999059],
           [0.83535021, 0.27729819, 0.49450273, 0.85165901, 0.81041096,
            0.87051101, 0.65315486],
           [0.2264058 , 0.70069179, 0.47573428, 0.74300094, 0.3600288 ,
            0.8437624 , 0.64245776],
           [0.51055178, 0.61533925, 0.07170028, 0.00528126, 0.73877679,
            0.00110946, 0.54102263],
           [0.93085316, 0.4567389 , 0.37350377, 0.05152994, 0.52306303,
            0.61123442, 0.43426194],
           [0.09055803, 0.64302116, 0.93807997, 0.86557746, 0.2043258 ,
            0.4361358 , 0.8844414 ],
           [0.37640475, 0.95720489, 0.05501881, 0.46798472, 0.75833743,
            0.61077986, 0.33906526]])




```python
dframe = pd.DataFrame(M , index=dates)
dframe
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>0.067289</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>0.870511</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>0.226406</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>0.843762</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>0.510552</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>0.930853</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>0.090558</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>0.204326</td>
      <td>0.436136</td>
      <td>0.884441</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>0.376405</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Changing Column Names
dframe.columns = ['C1' , 'C2' , 'C3', 'C4', 'C5', 'C6', 'C7']
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>0.067289</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>0.870511</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>0.226406</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>0.843762</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>0.510552</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>0.930853</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>0.090558</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>0.204326</td>
      <td>0.436136</td>
      <td>0.884441</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>0.376405</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
  </tbody>
</table>
</div>




```python
# List Index
dframe.index
```




    DatetimeIndex(['2020-01-20', '2020-01-21', '2020-01-22', '2020-01-23',
                   '2020-01-24', '2020-01-25', '2020-01-26'],
                  dtype='datetime64[ns]', freq='D')




```python
# List Column Names
dframe.columns
```




    Index(['C1', 'C2', 'C3', 'C4', 'C5', 'C6', 'C7'], dtype='object')




```python
# Datatype of each column
dframe.dtypes
```




    C1    float64
    C2    float64
    C3    float64
    C4    float64
    C5    float64
    C6    float64
    C7    float64
    dtype: object




```python
# Sort Dataframe by Column 'C1' in Ascending Order
dframe.sort_values(by='C1')
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-25</th>
      <td>0.090558</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>0.204326</td>
      <td>0.436136</td>
      <td>0.884441</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>0.226406</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>0.843762</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>0.376405</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>0.510552</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>0.067289</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>0.870511</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>0.930853</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sort Dataframe by Column 'C1' in Descending Order
dframe.sort_values(by='C1' , ascending=False)
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-24</th>
      <td>0.930853</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>0.870511</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>0.067289</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>0.510552</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>0.376405</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>0.226406</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>0.843762</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>0.090558</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>0.204326</td>
      <td>0.436136</td>
      <td>0.884441</td>
    </tr>
  </tbody>
</table>
</div>



## Delete Column in DataFrame


```python
df1
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Delete Column using "del" function
del df1['B']
```


```python
df1
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
      <th>A</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2.0</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3.0</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df5
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
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>row1</th>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>row2</th>
      <td>5</td>
      <td>10</td>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Delete Column using pop()
df5.pop('c')
```




    row1     NaN
    row2    20.0
    Name: c, dtype: float64




```python
df5
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
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>row1</th>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>row2</th>
      <td>5</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
dict = {'A' : pd.Series([1, 2, 3,11],    index=['a', 'b', 'c','d']),
        'B' : pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])}

df12 = pd.DataFrame(dict)
df12
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>d</th>
      <td>11</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df12.drop(['A'], axis=1,inplace=True)
df12
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
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3</td>
    </tr>
    <tr>
      <th>d</th>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



## Delete Rows in DataFrame


```python
col1 = np.linspace(10, 100, 30)
col2 = np.random.randint(10,100,30)
df10 = pd.DataFrame({"C1" : col1 , "C2" :col2})
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10.000000</td>
      <td>41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13.103448</td>
      <td>38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>16.206897</td>
      <td>42</td>
    </tr>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25.517241</td>
      <td>73</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
    <tr>
      <th>14</th>
      <td>53.448276</td>
      <td>94</td>
    </tr>
    <tr>
      <th>15</th>
      <td>56.551724</td>
      <td>45</td>
    </tr>
    <tr>
      <th>16</th>
      <td>59.655172</td>
      <td>59</td>
    </tr>
    <tr>
      <th>17</th>
      <td>62.758621</td>
      <td>32</td>
    </tr>
    <tr>
      <th>18</th>
      <td>65.862069</td>
      <td>70</td>
    </tr>
    <tr>
      <th>19</th>
      <td>68.965517</td>
      <td>60</td>
    </tr>
    <tr>
      <th>20</th>
      <td>72.068966</td>
      <td>90</td>
    </tr>
    <tr>
      <th>21</th>
      <td>75.172414</td>
      <td>73</td>
    </tr>
    <tr>
      <th>22</th>
      <td>78.275862</td>
      <td>88</td>
    </tr>
    <tr>
      <th>23</th>
      <td>81.379310</td>
      <td>38</td>
    </tr>
    <tr>
      <th>24</th>
      <td>84.482759</td>
      <td>27</td>
    </tr>
    <tr>
      <th>25</th>
      <td>87.586207</td>
      <td>69</td>
    </tr>
    <tr>
      <th>26</th>
      <td>90.689655</td>
      <td>47</td>
    </tr>
    <tr>
      <th>27</th>
      <td>93.793103</td>
      <td>21</td>
    </tr>
    <tr>
      <th>28</th>
      <td>96.896552</td>
      <td>28</td>
    </tr>
    <tr>
      <th>29</th>
      <td>100.000000</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Delete rows with index values 17,18,19
df10 = df10.drop([17,18,19], axis=0)
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10.000000</td>
      <td>41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13.103448</td>
      <td>38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>16.206897</td>
      <td>42</td>
    </tr>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25.517241</td>
      <td>73</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
    <tr>
      <th>14</th>
      <td>53.448276</td>
      <td>94</td>
    </tr>
    <tr>
      <th>15</th>
      <td>56.551724</td>
      <td>45</td>
    </tr>
    <tr>
      <th>16</th>
      <td>59.655172</td>
      <td>59</td>
    </tr>
    <tr>
      <th>20</th>
      <td>72.068966</td>
      <td>90</td>
    </tr>
    <tr>
      <th>21</th>
      <td>75.172414</td>
      <td>73</td>
    </tr>
    <tr>
      <th>22</th>
      <td>78.275862</td>
      <td>88</td>
    </tr>
    <tr>
      <th>23</th>
      <td>81.379310</td>
      <td>38</td>
    </tr>
    <tr>
      <th>24</th>
      <td>84.482759</td>
      <td>27</td>
    </tr>
    <tr>
      <th>25</th>
      <td>87.586207</td>
      <td>69</td>
    </tr>
    <tr>
      <th>26</th>
      <td>90.689655</td>
      <td>47</td>
    </tr>
    <tr>
      <th>27</th>
      <td>93.793103</td>
      <td>21</td>
    </tr>
    <tr>
      <th>28</th>
      <td>96.896552</td>
      <td>28</td>
    </tr>
    <tr>
      <th>29</th>
      <td>100.000000</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Delete rows with index values 16 without using assignment operation
df10.drop([16], axis=0,inplace=True)
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10.000000</td>
      <td>41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13.103448</td>
      <td>38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>16.206897</td>
      <td>42</td>
    </tr>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>5</th>
      <td>25.517241</td>
      <td>73</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
    <tr>
      <th>14</th>
      <td>53.448276</td>
      <td>94</td>
    </tr>
    <tr>
      <th>15</th>
      <td>56.551724</td>
      <td>45</td>
    </tr>
    <tr>
      <th>20</th>
      <td>72.068966</td>
      <td>90</td>
    </tr>
    <tr>
      <th>21</th>
      <td>75.172414</td>
      <td>73</td>
    </tr>
    <tr>
      <th>22</th>
      <td>78.275862</td>
      <td>88</td>
    </tr>
    <tr>
      <th>23</th>
      <td>81.379310</td>
      <td>38</td>
    </tr>
    <tr>
      <th>24</th>
      <td>84.482759</td>
      <td>27</td>
    </tr>
    <tr>
      <th>25</th>
      <td>87.586207</td>
      <td>69</td>
    </tr>
    <tr>
      <th>26</th>
      <td>90.689655</td>
      <td>47</td>
    </tr>
    <tr>
      <th>27</th>
      <td>93.793103</td>
      <td>21</td>
    </tr>
    <tr>
      <th>28</th>
      <td>96.896552</td>
      <td>28</td>
    </tr>
    <tr>
      <th>29</th>
      <td>100.000000</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
</div>




```python
df10.drop(df10.index[5] , inplace=True)
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10.000000</td>
      <td>41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13.103448</td>
      <td>38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>16.206897</td>
      <td>42</td>
    </tr>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
    <tr>
      <th>14</th>
      <td>53.448276</td>
      <td>94</td>
    </tr>
    <tr>
      <th>15</th>
      <td>56.551724</td>
      <td>45</td>
    </tr>
    <tr>
      <th>20</th>
      <td>72.068966</td>
      <td>90</td>
    </tr>
    <tr>
      <th>21</th>
      <td>75.172414</td>
      <td>73</td>
    </tr>
    <tr>
      <th>22</th>
      <td>78.275862</td>
      <td>88</td>
    </tr>
    <tr>
      <th>23</th>
      <td>81.379310</td>
      <td>38</td>
    </tr>
    <tr>
      <th>24</th>
      <td>84.482759</td>
      <td>27</td>
    </tr>
    <tr>
      <th>25</th>
      <td>87.586207</td>
      <td>69</td>
    </tr>
    <tr>
      <th>26</th>
      <td>90.689655</td>
      <td>47</td>
    </tr>
    <tr>
      <th>27</th>
      <td>93.793103</td>
      <td>21</td>
    </tr>
    <tr>
      <th>28</th>
      <td>96.896552</td>
      <td>28</td>
    </tr>
    <tr>
      <th>29</th>
      <td>100.000000</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Delete first three rows
df10 = df10.iloc[3:,]
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
    <tr>
      <th>14</th>
      <td>53.448276</td>
      <td>94</td>
    </tr>
    <tr>
      <th>15</th>
      <td>56.551724</td>
      <td>45</td>
    </tr>
    <tr>
      <th>20</th>
      <td>72.068966</td>
      <td>90</td>
    </tr>
    <tr>
      <th>21</th>
      <td>75.172414</td>
      <td>73</td>
    </tr>
    <tr>
      <th>22</th>
      <td>78.275862</td>
      <td>88</td>
    </tr>
    <tr>
      <th>23</th>
      <td>81.379310</td>
      <td>38</td>
    </tr>
    <tr>
      <th>24</th>
      <td>84.482759</td>
      <td>27</td>
    </tr>
    <tr>
      <th>25</th>
      <td>87.586207</td>
      <td>69</td>
    </tr>
    <tr>
      <th>26</th>
      <td>90.689655</td>
      <td>47</td>
    </tr>
    <tr>
      <th>27</th>
      <td>93.793103</td>
      <td>21</td>
    </tr>
    <tr>
      <th>28</th>
      <td>96.896552</td>
      <td>28</td>
    </tr>
    <tr>
      <th>29</th>
      <td>100.000000</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Delete last four rows
df10 = df10.iloc[:-4,]
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
    <tr>
      <th>14</th>
      <td>53.448276</td>
      <td>94</td>
    </tr>
    <tr>
      <th>15</th>
      <td>56.551724</td>
      <td>45</td>
    </tr>
    <tr>
      <th>20</th>
      <td>72.068966</td>
      <td>90</td>
    </tr>
    <tr>
      <th>21</th>
      <td>75.172414</td>
      <td>73</td>
    </tr>
    <tr>
      <th>22</th>
      <td>78.275862</td>
      <td>88</td>
    </tr>
    <tr>
      <th>23</th>
      <td>81.379310</td>
      <td>38</td>
    </tr>
    <tr>
      <th>24</th>
      <td>84.482759</td>
      <td>27</td>
    </tr>
    <tr>
      <th>25</th>
      <td>87.586207</td>
      <td>69</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Keep top 10 rows
df10 = df10.iloc[:10,]
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>




```python
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>




```python
df10.index[df10['C2'] == 56].tolist()
```




    []




```python
# Delete row based on Column value
df10.drop(df10.index[df10['C2'] == 56].tolist() , axis=0,inplace=True)
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Delete row based on Column value
df10 = df10.drop(df10[df10["C2"]==79].index)
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Delete all rows with column C2 value 14
df10 = df10[df10.C2 != 44]
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Delete all rows with column C2 value 88 & 55 using isin operator
df10 = df10[~(df10.C2.isin ([21,48]))]
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>19.310345</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22.413793</td>
      <td>88</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28.620690</td>
      <td>74</td>
    </tr>
    <tr>
      <th>7</th>
      <td>31.724138</td>
      <td>84</td>
    </tr>
    <tr>
      <th>8</th>
      <td>34.827586</td>
      <td>70</td>
    </tr>
    <tr>
      <th>9</th>
      <td>37.931034</td>
      <td>52</td>
    </tr>
    <tr>
      <th>10</th>
      <td>41.034483</td>
      <td>38</td>
    </tr>
    <tr>
      <th>11</th>
      <td>44.137931</td>
      <td>46</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47.241379</td>
      <td>62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>50.344828</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Keep all rows with column C2 value 10,89,31 & 64 using isin operator
df10 = df10[df10.C2.isin ([42,76])]
df10
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
      <th>C1</th>
      <th>C2</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
dict = {'A' : pd.Series([1, 2, 3,11],    index=['a', 'b', 'c','d']),
        'B' : pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])}

df11 = pd.DataFrame(dict)
df11
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>d</th>
      <td>11</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Delete all rows with label "d"
df11.drop("d", axis=0,inplace=True)
df11
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
df13 = pd.DataFrame({ 'ID' :[1,2,3,4] , 
                     'Name' :['Murilo' , 'Krominski' , 'Ross' , 'John'] , 
                     'location' : ['India' , 'Australia','UK' , 'US'] })
df13
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
      <th>ID</th>
      <th>Name</th>
      <th>location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
      <td>India</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
      <td>Australia</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Ross</td>
      <td>UK</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
      <td>US</td>
    </tr>
  </tbody>
</table>
</div>




```python
ind = df13[((df13.Name == 'Ross') &(df13.ID == 3) & (df13.location == 'UK'))].index
df13.drop(ind,inplace=True)
df13
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
      <th>ID</th>
      <th>Name</th>
      <th>location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
      <td>India</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
      <td>Australia</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
      <td>US</td>
    </tr>
  </tbody>
</table>
</div>



## Data Selection in Dataframe


```python
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
      <th>Language</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Java</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Python</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C++</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.index = [1,2,3,4]
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
      <th>Language</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Java</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Python</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C++</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Data selection using row label
df.loc[1]
```




    Language    Java
    Rating         1
    Name: 1, dtype: object




```python
# Data selection using position (Integer Index based)
df.iloc[1]
```




    Language    Python
    Rating           2
    Name: 2, dtype: object




```python
df.loc[1:2]
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
      <th>Language</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Java</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Python</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.iloc[1:2]
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
      <th>Language</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Python</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Data selection based on Condition
df.loc[df.Rating > 2]
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
      <th>Language</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>C</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C++</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1
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
      <th>A</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2.0</td>
    </tr>
    <tr>
      <th>c</th>
      <td>3.0</td>
    </tr>
    <tr>
      <th>d</th>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Row & Column label based selection
df1.loc['a']
```




    A    1.0
    Name: a, dtype: float64




```python
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>0.067289</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>0.870511</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>0.226406</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>0.843762</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>0.510552</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>0.930853</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>0.090558</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>0.204326</td>
      <td>0.436136</td>
      <td>0.884441</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>0.376405</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Data selection using Row Label
dframe['2020-01-20' : '2020-01-22' ]
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>0.067289</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>0.870511</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>0.226406</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>0.843762</td>
      <td>0.642458</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Selecting all rows & selected columns
dframe.loc[:,['C1' , 'C7']]
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
      <th>C1</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>0.226406</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>0.510552</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>0.930853</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>0.090558</td>
      <td>0.884441</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>0.376405</td>
      <td>0.339065</td>
    </tr>
  </tbody>
</table>
</div>




```python
#row & column label based selection
dframe.loc['2020-01-20' : '2020-01-22',['C1' , 'C7']]
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
      <th>C1</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>0.226406</td>
      <td>0.642458</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Data selection based on Condition
dframe[dframe['C1'] > 0.5]
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>0.067289</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>0.870511</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>0.510552</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>0.930853</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Data selection based on Condition
dframe[(dframe['C1'] > 0.5) & (dframe['C4'] > 0.5)]
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>0.067289</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>0.870511</td>
      <td>0.653155</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Data selection using position (Integer Index based)
dframe.iloc[0][0]
```




    0.7705324073693932




```python
# Select all rows & first three columns
dframe.iloc[:,0:3]
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>0.770532</td>
      <td>0.136053</td>
      <td>0.835822</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0.835350</td>
      <td>0.277298</td>
      <td>0.494503</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>0.226406</td>
      <td>0.700692</td>
      <td>0.475734</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>0.510552</td>
      <td>0.615339</td>
      <td>0.071700</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>0.930853</td>
      <td>0.456739</td>
      <td>0.373504</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>0.090558</td>
      <td>0.643021</td>
      <td>0.938080</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>0.376405</td>
      <td>0.957205</td>
      <td>0.055019</td>
    </tr>
  </tbody>
</table>
</div>




```python
dframe.iloc[0][0] = 10
```


```python
# Display all rows where C1 has value of 10 or 20
dframe[dframe['C1'].isin([10,20])]
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>10.0</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>0.067289</td>
      <td>0.419991</td>
    </tr>
  </tbody>
</table>
</div>



## Set Value


```python
# Set value of 888 for all elements in column 'C1'
dframe['C1'] = 888
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>0.067289</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>0.870511</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>0.843762</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>0.204326</td>
      <td>0.436136</td>
      <td>0.884441</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Set value of 777 for first three rows in Column 'C6'
dframe.at[0:3,'C6'] = 777
```


```python
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>0.835822</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>777.000000</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>777.000000</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>0.204326</td>
      <td>0.436136</td>
      <td>0.884441</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Set value of 333 in first row and third column
dframe.iat[0,2] = 333
```


```python
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>333.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>777.000000</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>777.000000</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>0.204326</td>
      <td>0.436136</td>
      <td>0.884441</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
  </tbody>
</table>
</div>




```python
dframe.iloc[0,2] = 555
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>777.000000</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>777.000000</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>0.204326</td>
      <td>0.436136</td>
      <td>0.884441</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create Copy of the calling objects data along with indices.
# Modifications to the data or indices of the copy will not be reflected in the original object 
dframe1 = dframe.copy(deep=True)
```


```python
dframe1[(dframe1['C1'] > 0.5) & (dframe1['C4'] > 0.5)] = 0
```


```python
dframe1[dframe1['C1'] == 0]
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Replace zeros in Column C1 with 99
dframe1[dframe1['C1'].isin([0])] = 99
dframe1
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>99</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>99</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>99</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>99</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
      <td>99.000000</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
  </tbody>
</table>
</div>




```python
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>777.000000</td>
      <td>0.419991</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>777.000000</td>
      <td>0.653155</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>0.642458</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>0.541023</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>0.434262</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>0.204326</td>
      <td>0.436136</td>
      <td>0.884441</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>0.339065</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Display all rows where value of C1 is 99
dframe1[dframe1['C1'] == 99]
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>99</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>99</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>99</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>99</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
      <td>99.0</td>
    </tr>
  </tbody>
</table>
</div>



## Dealing with NULL Values


```python
dframe.at[0:8 , 'C7'] = np.NaN
dframe.at[0:2 , 'C6'] = np.NaN
dframe.at[5:6 , 'C5'] = np.NaN
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>NaN</td>
      <td>0.436136</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Detect Non-Missing Values
# It will return True for NOT-NULL values and False for NULL values
dframe.notna()
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Detect Missing or NULL Values
# It will return True for NULL values and False for NOT-NULL values
dframe.isna()
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Fill all NULL values with 1020
dframe = dframe.fillna(1020)
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>1020.000000</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>1020.000000</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>1020.000000</td>
      <td>0.436136</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
dframe.at[0:5 , 'C7'] = np.NaN
dframe.at[0:2 , 'C6'] = np.NaN
dframe.at[5:6 , 'C5'] = np.NaN
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>NaN</td>
      <td>0.436136</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Replace Null values in Column 'C5' with number 123
# Replace Null values in Column 'C6' with number 789
dframe.fillna(value={'C5' : 123 , 'C6' : 789})
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>789.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>789.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>123.000000</td>
      <td>0.436136</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Replace first NULL value in Column C7 with 789
dframe.fillna(value={'C7' : 789} , limit=1)
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>NaN</td>
      <td>789.0</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>NaN</td>
      <td>0.436136</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop Rows with NULL values
dframe.dropna()
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.61078</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop Columns with NULL values
dframe.dropna(axis='columns')
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
    </tr>
  </tbody>
</table>
</div>




```python
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>NaN</td>
      <td>0.436136</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop Rows with NULL values present in C5 or C6
dframe.dropna(subset=['C5' ,'C6'])
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>



## Descriptive Statistics 


```python
# Fill NULL values with 55
dframe.fillna(55 , inplace=True)
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>55.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>55.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>888</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>888</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>888</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>55.000000</td>
      <td>0.436136</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Mean of all Columns
dframe.mean()
```




    C1    888.000000
    C2      0.540907
    C3     79.629791
    C4      0.524995
    C5      8.364673
    C6    126.951323
    C7    330.714286
    dtype: float64




```python
# Max value per column
dframe.max()
```




    C1     888.000000
    C2       0.957205
    C3     555.000000
    C4       0.865577
    C5      55.000000
    C6     777.000000
    C7    1020.000000
    dtype: float64




```python
# Min value per column
dframe.min()
```




    C1    888.000000
    C2      0.136053
    C3      0.055019
    C4      0.005281
    C5      0.360029
    C6      0.001109
    C7     55.000000
    dtype: float64




```python
# Median 
dframe.median()
```




    C1    888.000000
    C2      0.615339
    C3      0.475734
    C4      0.689934
    C5      0.738777
    C6      0.611234
    C7     55.000000
    dtype: float64




```python
dframe.std() #Standard Deviation
```




    C1      0.000000
    C2      0.275464
    C3    209.618770
    C4      0.363996
    C5     20.565091
    C6    287.797228
    C7    470.871785
    dtype: float64




```python
dframe.var()  #Variance 
```




    C1         0.000000
    C2         0.075880
    C3     43940.028795
    C4         0.132493
    C5       422.922954
    C6     82827.244728
    C7    221720.238095
    dtype: float64




```python
#Lower Quartile / First Quartile
dframe.quantile(0.25) 
```




    C1    888.000000
    C2      0.367019
    C3      0.222602
    C4      0.259757
    C5      0.442577
    C6      0.523458
    C7     55.000000
    Name: 0.25, dtype: float64




```python
#Second Quartile / Median
dframe.quantile(0.50)
```




    C1    888.000000
    C2      0.615339
    C3      0.475734
    C4      0.689934
    C5      0.738777
    C6      0.611234
    C7     55.000000
    Name: 0.5, dtype: float64




```python
# Upper Quartile
dframe.quantile(0.75)
```




    C1    888.000000
    C2      0.671856
    C3      0.716291
    C4      0.797330
    C5      0.784374
    C6     55.000000
    C7    537.500000
    Name: 0.75, dtype: float64




```python
 #IQR (Interquartile Range)
dframe.quantile(0.75) - dframe.quantile(0.25)
```




    C1      0.000000
    C2      0.304838
    C3      0.493689
    C4      0.537573
    C5      0.341797
    C6     54.476542
    C7    482.500000
    dtype: float64




```python
# SUM of column values
dframe.sum()
```




    C1    6216.000000
    C2       3.786347
    C3     557.408540
    C4       3.674967
    C5      58.552708
    C6     888.659260
    C7    2315.000000
    dtype: float64




```python
# GENERATES DESCRIPTIVE STATS
dframe.describe()
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>7.0</td>
      <td>7.000000</td>
      <td>7.000000</td>
      <td>7.000000</td>
      <td>7.000000</td>
      <td>7.000000</td>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>888.0</td>
      <td>0.540907</td>
      <td>79.629791</td>
      <td>0.524995</td>
      <td>8.364673</td>
      <td>126.951323</td>
      <td>330.714286</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.0</td>
      <td>0.275464</td>
      <td>209.618770</td>
      <td>0.363996</td>
      <td>20.565091</td>
      <td>287.797228</td>
      <td>470.871785</td>
    </tr>
    <tr>
      <th>min</th>
      <td>888.0</td>
      <td>0.136053</td>
      <td>0.055019</td>
      <td>0.005281</td>
      <td>0.360029</td>
      <td>0.001109</td>
      <td>55.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>888.0</td>
      <td>0.367019</td>
      <td>0.222602</td>
      <td>0.259757</td>
      <td>0.442577</td>
      <td>0.523458</td>
      <td>55.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>888.0</td>
      <td>0.615339</td>
      <td>0.475734</td>
      <td>0.689934</td>
      <td>0.738777</td>
      <td>0.611234</td>
      <td>55.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>888.0</td>
      <td>0.671856</td>
      <td>0.716291</td>
      <td>0.797330</td>
      <td>0.784374</td>
      <td>55.000000</td>
      <td>537.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>888.0</td>
      <td>0.957205</td>
      <td>555.000000</td>
      <td>0.865577</td>
      <td>55.000000</td>
      <td>777.000000</td>
      <td>1020.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Return unbiased skew
# https://www.youtube.com/watch?v=HnMGKsupF8Q
dframe.skew()
```




    C1    0.000000
    C2   -0.084499
    C3    2.645740
    C4   -0.761952
    C5    2.645295
    C6    2.602155
    C7    1.229634
    dtype: float64




```python
# Return unbiased kurtosis using Fisher’s definition of kurtosis
# https://www.youtube.com/watch?v=HnMGKsupF8Q
dframe.kurt()
```




    C1    0.000000
    C2   -0.328790
    C3    6.999955
    C4   -1.384257
    C5    6.998162
    C6    6.819700
    C7   -0.840000
    dtype: float64




```python
#Correlation
# https://www.youtube.com/watch?v=qtaqvPAeEJY&list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9&index=10
# https://www.youtube.com/watch?v=xZ_z8KWkhXE&list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9&index=11
dframe.corr()
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>C1</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>C2</th>
      <td>NaN</td>
      <td>1.000000</td>
      <td>-0.648441</td>
      <td>-0.175931</td>
      <td>0.165940</td>
      <td>0.184236</td>
      <td>0.642812</td>
    </tr>
    <tr>
      <th>C3</th>
      <td>NaN</td>
      <td>-0.648441</td>
      <td>1.000000</td>
      <td>0.200760</td>
      <td>-0.170467</td>
      <td>-0.110069</td>
      <td>-0.257889</td>
    </tr>
    <tr>
      <th>C4</th>
      <td>NaN</td>
      <td>-0.175931</td>
      <td>0.200760</td>
      <td>1.000000</td>
      <td>0.411013</td>
      <td>0.312234</td>
      <td>0.266097</td>
    </tr>
    <tr>
      <th>C5</th>
      <td>NaN</td>
      <td>0.165940</td>
      <td>-0.170467</td>
      <td>0.411013</td>
      <td>1.000000</td>
      <td>-0.198931</td>
      <td>0.648231</td>
    </tr>
    <tr>
      <th>C6</th>
      <td>NaN</td>
      <td>0.184236</td>
      <td>-0.110069</td>
      <td>0.312234</td>
      <td>-0.198931</td>
      <td>1.000000</td>
      <td>-0.300096</td>
    </tr>
    <tr>
      <th>C7</th>
      <td>NaN</td>
      <td>0.642812</td>
      <td>-0.257889</td>
      <td>0.266097</td>
      <td>0.648231</td>
      <td>-0.300096</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Covariance
# https://www.youtube.com/watch?v=qtaqvPAeEJY&list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9&index=10
# https://www.youtube.com/watch?v=xZ_z8KWkhXE&list=PLblh5JKOoLUK0FLuzwntyYI10UQFUhsY9&index=11
dframe.cov()
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>C1</th>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>C2</th>
      <td>0.0</td>
      <td>0.075880</td>
      <td>-37.442571</td>
      <td>-0.017640</td>
      <td>0.940042</td>
      <td>14.605829</td>
      <td>83.378008</td>
    </tr>
    <tr>
      <th>C3</th>
      <td>0.0</td>
      <td>-37.442571</td>
      <td>43940.028795</td>
      <td>15.318072</td>
      <td>-734.853812</td>
      <td>-6640.206195</td>
      <td>-25454.526182</td>
    </tr>
    <tr>
      <th>C4</th>
      <td>0.0</td>
      <td>-0.017640</td>
      <td>15.318072</td>
      <td>0.132493</td>
      <td>3.076687</td>
      <td>32.708706</td>
      <td>45.607755</td>
    </tr>
    <tr>
      <th>C5</th>
      <td>0.0</td>
      <td>0.940042</td>
      <td>-734.853812</td>
      <td>3.076687</td>
      <td>422.922954</td>
      <td>-1177.390430</td>
      <td>6277.162920</td>
    </tr>
    <tr>
      <th>C6</th>
      <td>0.0</td>
      <td>14.605829</td>
      <td>-6640.206195</td>
      <td>32.708706</td>
      <td>-1177.390430</td>
      <td>82827.244728</td>
      <td>-40667.629896</td>
    </tr>
    <tr>
      <th>C7</th>
      <td>0.0</td>
      <td>83.378008</td>
      <td>-25454.526182</td>
      <td>45.607755</td>
      <td>6277.162920</td>
      <td>-40667.629896</td>
      <td>221720.238095</td>
    </tr>
  </tbody>
</table>
</div>




```python
import statistics as st
dframe.at[3:6,'C1'] = 22
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>55.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>55.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>22</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>22</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>22</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>55.000000</td>
      <td>0.436136</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Average 
st.mean(dframe['C1'])
```




    516.8571428571429




```python
# Hormonic Mean
st.harmonic_mean(dframe['C1'])
```




    49.69186046511628




```python
#Returns average of the two middle numbers when length is EVEN
arr = np.array([1,2,3,4,5,6,7,8])
st.median(arr)
```




    4.5




```python
# low median of the data with EVEN length
st.median_low(arr)
```




    4




```python
# High median of the data with EVEN length
st.median_high(arr)
```




    5




```python
# Mode of Dataset
st.mode(dframe['C7'])
```




    55.0




```python
# Sample Variance
st.variance(dframe['C1'])
```




    214273.14285714287




```python
#Population Variance
st.pvariance(dframe['C1'])
```




    183662.69387755104




```python
#Sample  Standard Deviation
st.stdev(dframe['C1'])
```




    462.89647099231905




```python
#Population Standard Deviation
st.pstdev(dframe['C1'])
```




    428.5588569584708



## Apply function on Dataframe


```python
dframe
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>55.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>55.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>22</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>22</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>22</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>55.000000</td>
      <td>0.436136</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Finding MAX value in Columns
dframe.apply(max)
```




    C1     888.000000
    C2       0.957205
    C3     555.000000
    C4       0.865577
    C5      55.000000
    C6     777.000000
    C7    1020.000000
    dtype: float64




```python
# Finding minimum value in Columns
dframe.apply(min)
```




    C1    22.000000
    C2     0.136053
    C3     0.055019
    C4     0.005281
    C5     0.360029
    C6     0.001109
    C7    55.000000
    dtype: float64




```python
#Sum of Column Values
dframe.apply(sum)
```




    C1    3618.000000
    C2       3.786347
    C3     557.408540
    C4       3.674967
    C5      58.552708
    C6     888.659260
    C7    2315.000000
    dtype: float64




```python
#Sum of Column Values
dframe.apply(np.sum)
```




    C1    3618.000000
    C2       3.786347
    C3     557.408540
    C4       3.674967
    C5      58.552708
    C6     888.659260
    C7    2315.000000
    dtype: float64




```python
# Sum of rows
dframe.apply(np.sum ,axis=1)
```




    2020-01-20    1554.188078
    2020-01-21    1000.433871
    2020-01-22    1722.279456
    2020-01-23      78.432207
    2020-01-24      79.016070
    2020-01-25    1099.882814
    2020-01-26    1910.849326
    Freq: D, dtype: float64




```python
# Square root of all values in a DataFrame
dframe.applymap(np.sqrt)
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>29.799329</td>
      <td>0.368854</td>
      <td>23.558438</td>
      <td>0.830623</td>
      <td>0.601740</td>
      <td>7.416198</td>
      <td>7.416198</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>29.799329</td>
      <td>0.526591</td>
      <td>0.703209</td>
      <td>0.922854</td>
      <td>0.900228</td>
      <td>7.416198</td>
      <td>7.416198</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>29.799329</td>
      <td>0.837073</td>
      <td>0.689735</td>
      <td>0.861975</td>
      <td>0.600024</td>
      <td>27.874720</td>
      <td>7.416198</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>4.690416</td>
      <td>0.784436</td>
      <td>0.267769</td>
      <td>0.072672</td>
      <td>0.859521</td>
      <td>0.033309</td>
      <td>7.416198</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>4.690416</td>
      <td>0.675825</td>
      <td>0.611150</td>
      <td>0.227002</td>
      <td>0.723231</td>
      <td>0.781815</td>
      <td>7.416198</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>4.690416</td>
      <td>0.801886</td>
      <td>0.968545</td>
      <td>0.930364</td>
      <td>7.416198</td>
      <td>0.660406</td>
      <td>31.937439</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>29.799329</td>
      <td>0.978368</td>
      <td>0.234561</td>
      <td>0.684094</td>
      <td>0.870826</td>
      <td>0.781524</td>
      <td>31.937439</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Square root of all values in a DataFrame
dframe.applymap(math.sqrt)
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>29.799329</td>
      <td>0.368854</td>
      <td>23.558438</td>
      <td>0.830623</td>
      <td>0.601740</td>
      <td>7.416198</td>
      <td>7.416198</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>29.799329</td>
      <td>0.526591</td>
      <td>0.703209</td>
      <td>0.922854</td>
      <td>0.900228</td>
      <td>7.416198</td>
      <td>7.416198</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>29.799329</td>
      <td>0.837073</td>
      <td>0.689735</td>
      <td>0.861975</td>
      <td>0.600024</td>
      <td>27.874720</td>
      <td>7.416198</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>4.690416</td>
      <td>0.784436</td>
      <td>0.267769</td>
      <td>0.072672</td>
      <td>0.859521</td>
      <td>0.033309</td>
      <td>7.416198</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>4.690416</td>
      <td>0.675825</td>
      <td>0.611150</td>
      <td>0.227002</td>
      <td>0.723231</td>
      <td>0.781815</td>
      <td>7.416198</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>4.690416</td>
      <td>0.801886</td>
      <td>0.968545</td>
      <td>0.930364</td>
      <td>7.416198</td>
      <td>0.660406</td>
      <td>31.937439</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>29.799329</td>
      <td>0.978368</td>
      <td>0.234561</td>
      <td>0.684094</td>
      <td>0.870826</td>
      <td>0.781524</td>
      <td>31.937439</td>
    </tr>
  </tbody>
</table>
</div>




```python
dframe.applymap(float)
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>888.0</td>
      <td>0.136053</td>
      <td>555.000000</td>
      <td>0.689934</td>
      <td>0.362091</td>
      <td>55.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>888.0</td>
      <td>0.277298</td>
      <td>0.494503</td>
      <td>0.851659</td>
      <td>0.810411</td>
      <td>55.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>888.0</td>
      <td>0.700692</td>
      <td>0.475734</td>
      <td>0.743001</td>
      <td>0.360029</td>
      <td>777.000000</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>22.0</td>
      <td>0.615339</td>
      <td>0.071700</td>
      <td>0.005281</td>
      <td>0.738777</td>
      <td>0.001109</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>22.0</td>
      <td>0.456739</td>
      <td>0.373504</td>
      <td>0.051530</td>
      <td>0.523063</td>
      <td>0.611234</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>22.0</td>
      <td>0.643021</td>
      <td>0.938080</td>
      <td>0.865577</td>
      <td>55.000000</td>
      <td>0.436136</td>
      <td>1020.0</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>888.0</td>
      <td>0.957205</td>
      <td>0.055019</td>
      <td>0.467985</td>
      <td>0.758337</td>
      <td>0.610780</td>
      <td>1020.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using Lambda function in Dataframes
dframe.apply(lambda x: min(x))
```




    C1    22.000000
    C2     0.136053
    C3     0.055019
    C4     0.005281
    C5     0.360029
    C6     0.001109
    C7    55.000000
    dtype: float64




```python
# Using Lambda function in Dataframes
dframe.apply(lambda x: x*x)
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
      <th>C1</th>
      <th>C2</th>
      <th>C3</th>
      <th>C4</th>
      <th>C5</th>
      <th>C6</th>
      <th>C7</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-20</th>
      <td>788544</td>
      <td>0.018510</td>
      <td>308025.000000</td>
      <td>0.476009</td>
      <td>0.131110</td>
      <td>3025.000000</td>
      <td>3025.0</td>
    </tr>
    <tr>
      <th>2020-01-21</th>
      <td>788544</td>
      <td>0.076894</td>
      <td>0.244533</td>
      <td>0.725323</td>
      <td>0.656766</td>
      <td>3025.000000</td>
      <td>3025.0</td>
    </tr>
    <tr>
      <th>2020-01-22</th>
      <td>788544</td>
      <td>0.490969</td>
      <td>0.226323</td>
      <td>0.552050</td>
      <td>0.129621</td>
      <td>603729.000000</td>
      <td>3025.0</td>
    </tr>
    <tr>
      <th>2020-01-23</th>
      <td>484</td>
      <td>0.378642</td>
      <td>0.005141</td>
      <td>0.000028</td>
      <td>0.545791</td>
      <td>0.000001</td>
      <td>3025.0</td>
    </tr>
    <tr>
      <th>2020-01-24</th>
      <td>484</td>
      <td>0.208610</td>
      <td>0.139505</td>
      <td>0.002655</td>
      <td>0.273595</td>
      <td>0.373608</td>
      <td>3025.0</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>484</td>
      <td>0.413476</td>
      <td>0.879994</td>
      <td>0.749224</td>
      <td>3025.000000</td>
      <td>0.190214</td>
      <td>1040400.0</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>788544</td>
      <td>0.916241</td>
      <td>0.003027</td>
      <td>0.219010</td>
      <td>0.575076</td>
      <td>0.373052</td>
      <td>1040400.0</td>
    </tr>
  </tbody>
</table>
</div>



# Merge Dataframes


```python
daf1 =  pd.DataFrame ({'id': ['1', '2', '3', '4', '5'], 'Name': ['Murilo', 'Krominski', 'Bran', 'John', 'David']})
daf1
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
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Bran</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>David</td>
    </tr>
  </tbody>
</table>
</div>




```python
daf2 =  pd.DataFrame ({'id': ['1', '2', '6', '7', '8'], 'Score': [40 , 60 , 80 , 90 , 70]})
daf2
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
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8</td>
      <td>70</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Inner Join
pd.merge(daf1, daf2, on='id', how='inner')
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
      <th>Name</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
      <td>60</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Full Outer Join
pd.merge(daf1, daf2, on='id', how='outer')
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
      <th>Name</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Bran</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>David</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>NaN</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>NaN</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>NaN</td>
      <td>70.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Left Outer Join
pd.merge(daf1, daf2, on='id', how='left')
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
      <th>Name</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Bran</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>David</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Right Outer Join
pd.merge(daf1, daf2, on='id', how='right')
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
      <th>Name</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>NaN</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>NaN</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8</td>
      <td>NaN</td>
      <td>70</td>
    </tr>
  </tbody>
</table>
</div>



# Importing multiple CSV files in DataFrame


```python
# Append all CSV files 
path =r'/content/Exemplo'
filenames = glob.glob(path + "/*.csv")
covid = pd.DataFrame()
for f in filenames:
    df = pd.read_csv(f)
    covid = covid.append(df,ignore_index=True,sort=True)
```


```python
filenames
```




    ['/content/Exemplo/02-01-2020.csv',
     '/content/Exemplo/02-05-2020.csv',
     '/content/Exemplo/02-02-2020.csv',
     '/content/Exemplo/02-04-2020.csv',
     '/content/Exemplo/02-03-2020.csv']




```python
# Top 10 rows of the Dataframe
covid.head(10)
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
      <th>Confirmed</th>
      <th>Country/Region</th>
      <th>Deaths</th>
      <th>Last Update</th>
      <th>Province/State</th>
      <th>Recovered</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7153</td>
      <td>Mainland China</td>
      <td>249</td>
      <td>2/1/2020 11:53</td>
      <td>Hubei</td>
      <td>168</td>
    </tr>
    <tr>
      <th>1</th>
      <td>599</td>
      <td>Mainland China</td>
      <td>0</td>
      <td>2/1/2020 10:53</td>
      <td>Zhejiang</td>
      <td>21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>535</td>
      <td>Mainland China</td>
      <td>0</td>
      <td>2/1/2020 14:23</td>
      <td>Guangdong</td>
      <td>14</td>
    </tr>
    <tr>
      <th>3</th>
      <td>422</td>
      <td>Mainland China</td>
      <td>2</td>
      <td>2/1/2020 1:52</td>
      <td>Henan</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>389</td>
      <td>Mainland China</td>
      <td>0</td>
      <td>2/1/2020 11:03</td>
      <td>Hunan</td>
      <td>8</td>
    </tr>
    <tr>
      <th>5</th>
      <td>297</td>
      <td>Mainland China</td>
      <td>0</td>
      <td>2/1/2020 13:33</td>
      <td>Anhui</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>286</td>
      <td>Mainland China</td>
      <td>0</td>
      <td>2/1/2020 1:52</td>
      <td>Jiangxi</td>
      <td>9</td>
    </tr>
    <tr>
      <th>7</th>
      <td>247</td>
      <td>Mainland China</td>
      <td>1</td>
      <td>2/1/2020 8:43</td>
      <td>Chongqing</td>
      <td>3</td>
    </tr>
    <tr>
      <th>8</th>
      <td>207</td>
      <td>Mainland China</td>
      <td>1</td>
      <td>2/1/2020 1:52</td>
      <td>Sichuan</td>
      <td>3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>206</td>
      <td>Mainland China</td>
      <td>0</td>
      <td>2/1/2020 7:51</td>
      <td>Shandong</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Bottom 10 rows of the Dataframe
covid.tail(10)
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
      <th>Confirmed</th>
      <th>Country/Region</th>
      <th>Deaths</th>
      <th>Last Update</th>
      <th>Province/State</th>
      <th>Recovered</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>333</th>
      <td>1</td>
      <td>Mainland China</td>
      <td>0</td>
      <td>2020-02-01T01:52:40</td>
      <td>Tibet</td>
      <td>0</td>
    </tr>
    <tr>
      <th>334</th>
      <td>1</td>
      <td>Nepal</td>
      <td>0</td>
      <td>2020-01-31T08:15:53</td>
      <td>NaN</td>
      <td>0</td>
    </tr>
    <tr>
      <th>335</th>
      <td>1</td>
      <td>Spain</td>
      <td>0</td>
      <td>2020-02-01T23:43:02</td>
      <td>NaN</td>
      <td>0</td>
    </tr>
    <tr>
      <th>336</th>
      <td>1</td>
      <td>Sri Lanka</td>
      <td>0</td>
      <td>2020-01-31T08:15:53</td>
      <td>NaN</td>
      <td>0</td>
    </tr>
    <tr>
      <th>337</th>
      <td>1</td>
      <td>Sweden</td>
      <td>0</td>
      <td>2020-02-01T02:13:26</td>
      <td>NaN</td>
      <td>0</td>
    </tr>
    <tr>
      <th>338</th>
      <td>1</td>
      <td>US</td>
      <td>0</td>
      <td>2020-02-01T19:43:03</td>
      <td>Boston, MA</td>
      <td>0</td>
    </tr>
    <tr>
      <th>339</th>
      <td>1</td>
      <td>US</td>
      <td>0</td>
      <td>2020-02-01T19:53:03</td>
      <td>Los Angeles, CA</td>
      <td>0</td>
    </tr>
    <tr>
      <th>340</th>
      <td>1</td>
      <td>US</td>
      <td>0</td>
      <td>2020-02-01T19:53:03</td>
      <td>Orange, CA</td>
      <td>0</td>
    </tr>
    <tr>
      <th>341</th>
      <td>1</td>
      <td>US</td>
      <td>0</td>
      <td>2020-02-01T19:43:03</td>
      <td>Seattle, WA</td>
      <td>0</td>
    </tr>
    <tr>
      <th>342</th>
      <td>1</td>
      <td>US</td>
      <td>0</td>
      <td>2020-02-01T19:43:03</td>
      <td>Tempe, AZ</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Unique values in Country column
covid['Country/Region'].unique()
```




    array(['Mainland China', 'Japan', 'Thailand', 'Singapore', 'Hong Kong',
           'South Korea', 'Taiwan', 'Malaysia', 'Germany', 'Macau', 'France',
           'Vietnam', 'Australia', 'United Arab Emirates', 'Canada', 'Italy',
           'Russia', 'UK', 'US', 'Cambodia', 'Finland', 'India', 'Nepal',
           'Philippines', 'Spain', 'Sri Lanka', 'Sweden', 'Belgium'],
          dtype=object)




```python
# Number of Unique values in Country column
covid['Country/Region'].nunique()
```




    28




```python
#Dataframe information
covid.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 343 entries, 0 to 342
    Data columns (total 6 columns):
     #   Column          Non-Null Count  Dtype 
    ---  ------          --------------  ----- 
     0   Confirmed       343 non-null    int64 
     1   Country/Region  343 non-null    object
     2   Deaths          343 non-null    int64 
     3   Last Update     343 non-null    object
     4   Province/State  241 non-null    object
     5   Recovered       343 non-null    int64 
    dtypes: int64(3), object(3)
    memory usage: 16.2+ KB
    


```python
# Reading columns
covid['Country/Region'].head(10)
```




    0    Mainland China
    1    Mainland China
    2    Mainland China
    3    Mainland China
    4    Mainland China
    5    Mainland China
    6    Mainland China
    7    Mainland China
    8    Mainland China
    9    Mainland China
    Name: Country/Region, dtype: object




```python
# Reading columns
df1 = covid[['Country/Region' ,'Province/State','Confirmed' , 'Last Update']]
df1.head(10)
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
      <th>Country/Region</th>
      <th>Province/State</th>
      <th>Confirmed</th>
      <th>Last Update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mainland China</td>
      <td>Hubei</td>
      <td>7153</td>
      <td>2/1/2020 11:53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mainland China</td>
      <td>Zhejiang</td>
      <td>599</td>
      <td>2/1/2020 10:53</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mainland China</td>
      <td>Guangdong</td>
      <td>535</td>
      <td>2/1/2020 14:23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mainland China</td>
      <td>Henan</td>
      <td>422</td>
      <td>2/1/2020 1:52</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Mainland China</td>
      <td>Hunan</td>
      <td>389</td>
      <td>2/1/2020 11:03</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Mainland China</td>
      <td>Anhui</td>
      <td>297</td>
      <td>2/1/2020 13:33</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Mainland China</td>
      <td>Jiangxi</td>
      <td>286</td>
      <td>2/1/2020 1:52</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Mainland China</td>
      <td>Chongqing</td>
      <td>247</td>
      <td>2/1/2020 8:43</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Mainland China</td>
      <td>Sichuan</td>
      <td>207</td>
      <td>2/1/2020 1:52</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Mainland China</td>
      <td>Shandong</td>
      <td>206</td>
      <td>2/1/2020 7:51</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Read specific rows 
df1.iloc[1:4]
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
      <th>Country/Region</th>
      <th>Province/State</th>
      <th>Confirmed</th>
      <th>Last Update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Mainland China</td>
      <td>Zhejiang</td>
      <td>599</td>
      <td>2/1/2020 10:53</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mainland China</td>
      <td>Guangdong</td>
      <td>535</td>
      <td>2/1/2020 14:23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mainland China</td>
      <td>Henan</td>
      <td>422</td>
      <td>2/1/2020 1:52</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Filter data 
df1.loc[df1['Country/Region']== 'India']
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
      <th>Country/Region</th>
      <th>Province/State</th>
      <th>Confirmed</th>
      <th>Last Update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>54</th>
      <td>India</td>
      <td>NaN</td>
      <td>1</td>
      <td>1/31/2020 8:15</td>
    </tr>
    <tr>
      <th>112</th>
      <td>India</td>
      <td>NaN</td>
      <td>3</td>
      <td>2020-02-03T21:43:02</td>
    </tr>
    <tr>
      <th>185</th>
      <td>India</td>
      <td>NaN</td>
      <td>2</td>
      <td>2020-02-02T06:03:08</td>
    </tr>
    <tr>
      <th>250</th>
      <td>India</td>
      <td>NaN</td>
      <td>3</td>
      <td>2020-02-03T21:43:02</td>
    </tr>
    <tr>
      <th>320</th>
      <td>India</td>
      <td>NaN</td>
      <td>3</td>
      <td>2020-02-03T21:43:02</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Sort Data Frame
display('Sorted Data Frame', df1.sort_values(['Country/Region'], ascending=True).head(5))
```


    'Sorted Data Frame'



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
      <th>Country/Region</th>
      <th>Province/State</th>
      <th>Confirmed</th>
      <th>Last Update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>50</th>
      <td>Australia</td>
      <td>South Australia</td>
      <td>1</td>
      <td>2/1/2020 18:12</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Australia</td>
      <td>Queensland</td>
      <td>3</td>
      <td>2/1/2020 18:12</td>
    </tr>
    <tr>
      <th>322</th>
      <td>Australia</td>
      <td>South Australia</td>
      <td>2</td>
      <td>2020-02-02T22:33:07</td>
    </tr>
    <tr>
      <th>321</th>
      <td>Australia</td>
      <td>Queensland</td>
      <td>2</td>
      <td>2020-02-02T22:33:07</td>
    </tr>
    <tr>
      <th>318</th>
      <td>Australia</td>
      <td>Victoria</td>
      <td>4</td>
      <td>2020-02-01T18:12:49</td>
    </tr>
  </tbody>
</table>
</div>



```python
#Sort Data Frame
display('Sorted Data Frame', df1.sort_values(['Country/Region'], ascending=False).head(5))
```


    'Sorted Data Frame'



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
      <th>Country/Region</th>
      <th>Province/State</th>
      <th>Confirmed</th>
      <th>Last Update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>244</th>
      <td>Vietnam</td>
      <td>NaN</td>
      <td>8</td>
      <td>2020-02-03T21:43:02</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Vietnam</td>
      <td>NaN</td>
      <td>6</td>
      <td>2/1/2020 7:38</td>
    </tr>
    <tr>
      <th>106</th>
      <td>Vietnam</td>
      <td>NaN</td>
      <td>8</td>
      <td>2020-02-03T21:43:02</td>
    </tr>
    <tr>
      <th>178</th>
      <td>Vietnam</td>
      <td>NaN</td>
      <td>6</td>
      <td>2020-02-01T07:38:12</td>
    </tr>
    <tr>
      <th>314</th>
      <td>Vietnam</td>
      <td>NaN</td>
      <td>8</td>
      <td>2020-02-03T21:43:02</td>
    </tr>
  </tbody>
</table>
</div>



```python
#Sort Data Frame - Ascending on "Country" & descending on "Last update"
display('Sorted Data Frame', df1.sort_values(['Country/Region', 'Last Update'], ascending=[1,0]).head(5))
```


    'Sorted Data Frame'



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
      <th>Country/Region</th>
      <th>Province/State</th>
      <th>Confirmed</th>
      <th>Last Update</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>111</th>
      <td>Australia</td>
      <td>Queensland</td>
      <td>3</td>
      <td>2020-02-04T16:53:03</td>
    </tr>
    <tr>
      <th>249</th>
      <td>Australia</td>
      <td>Queensland</td>
      <td>3</td>
      <td>2020-02-04T16:53:03</td>
    </tr>
    <tr>
      <th>113</th>
      <td>Australia</td>
      <td>South Australia</td>
      <td>2</td>
      <td>2020-02-02T22:33:07</td>
    </tr>
    <tr>
      <th>183</th>
      <td>Australia</td>
      <td>Queensland</td>
      <td>2</td>
      <td>2020-02-02T22:33:07</td>
    </tr>
    <tr>
      <th>184</th>
      <td>Australia</td>
      <td>South Australia</td>
      <td>2</td>
      <td>2020-02-02T22:33:07</td>
    </tr>
  </tbody>
</table>
</div>



```python
#Iterating through the dataset
for index , row in df1.iterrows():
    if (row['Country/Region'] == 'Indonesia' ):
        display(row[['Country/Region' ,'Confirmed']])
```


```python
#Unique Values
covid['Country/Region'].drop_duplicates(keep='first').head(10)
```




    0     Mainland China
    27             Japan
    28          Thailand
    31         Singapore
    32         Hong Kong
    33       South Korea
    34            Taiwan
    36          Malaysia
    37           Germany
    38             Macau
    Name: Country/Region, dtype: object




```python
# Countries impacted with Coronavirus
countries = covid['Country/Region'].unique()
type(countries) , countries
```




    (numpy.ndarray,
     array(['Mainland China', 'Japan', 'Thailand', 'Singapore', 'Hong Kong',
            'South Korea', 'Taiwan', 'Malaysia', 'Germany', 'Macau', 'France',
            'Vietnam', 'Australia', 'United Arab Emirates', 'Canada', 'Italy',
            'Russia', 'UK', 'US', 'Cambodia', 'Finland', 'India', 'Nepal',
            'Philippines', 'Spain', 'Sri Lanka', 'Sweden', 'Belgium'],
           dtype=object))




```python
df2 = pd.read_csv('/content/Exemplo2/pokemon.csv')
df2.head(5)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sum of Columns 
df2['Total'] = df2['HP'] + df2['Attack']
df2.head(5)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>94</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>122</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>162</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>180</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>91</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sum of Columns 
df2['Total'] = df2.iloc[:,4:10].sum(axis=1)
df2.head(5)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Shifting "Total" column

cols = list(df2.columns)

df2 = df2[cols[0:10] + [cols[-1]] + cols[10:12]]
df2.head(5)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Legendary</th>
      <th>Speed</th>
      <th>Generation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>False</td>
      <td>45</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>False</td>
      <td>60</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>False</td>
      <td>80</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>False</td>
      <td>80</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>False</td>
      <td>65</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Shifting "Legendary" column -  Index location -1 or 12

cols = list(df2.columns)

df2 = df2[cols[0:10] + [cols[-1]] + cols[10:12]]
df2.head(5)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
      <td>45</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>1</td>
      <td>False</td>
      <td>80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>1</td>
      <td>False</td>
      <td>65</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Shifting "Generation" column - Index location -1 or 12

cols = list(df2.columns)

df2 = df2[cols[0:10] + [cols[12]] + cols[10:12]]
df2.head(5)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Save to CSV file

df2.to_csv('poke_updated.csv')
```


```python
#Save to CSV file without index column

df2.to_csv('poke_updated1.csv', index=False)
```


```python
df2.head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>447</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>596</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Fire</td>
      <td>Dragon</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>716</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Save Dataframe as text file
df2.to_csv('poke.txt' , sep='\t' , index=False)
```


```python
# Save Dataframe as xlsx file
df2.to_excel('poke.xlsx')
```


```python
# Save Dataframe as xlsx file without row names
df2.to_excel('poke.xlsx', index=0)
```


```python
#Filtering using loc

df2.loc[df2['Type 2'] == 'Dragon']
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Fire</td>
      <td>Dragon</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>196</th>
      <td>181</td>
      <td>AmpharosMega Ampharos</td>
      <td>Electric</td>
      <td>Dragon</td>
      <td>750</td>
      <td>90</td>
      <td>95</td>
      <td>105</td>
      <td>165</td>
      <td>110</td>
      <td>45</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>249</th>
      <td>230</td>
      <td>Kingdra</td>
      <td>Water</td>
      <td>Dragon</td>
      <td>625</td>
      <td>75</td>
      <td>95</td>
      <td>95</td>
      <td>95</td>
      <td>95</td>
      <td>85</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>275</th>
      <td>254</td>
      <td>SceptileMega Sceptile</td>
      <td>Grass</td>
      <td>Dragon</td>
      <td>665</td>
      <td>70</td>
      <td>110</td>
      <td>75</td>
      <td>145</td>
      <td>85</td>
      <td>145</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>360</th>
      <td>329</td>
      <td>Vibrava</td>
      <td>Ground</td>
      <td>Dragon</td>
      <td>390</td>
      <td>50</td>
      <td>70</td>
      <td>50</td>
      <td>50</td>
      <td>50</td>
      <td>70</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>361</th>
      <td>330</td>
      <td>Flygon</td>
      <td>Ground</td>
      <td>Dragon</td>
      <td>600</td>
      <td>80</td>
      <td>100</td>
      <td>80</td>
      <td>80</td>
      <td>80</td>
      <td>100</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>540</th>
      <td>483</td>
      <td>Dialga</td>
      <td>Steel</td>
      <td>Dragon</td>
      <td>810</td>
      <td>100</td>
      <td>120</td>
      <td>120</td>
      <td>150</td>
      <td>100</td>
      <td>90</td>
      <td>4</td>
      <td>True</td>
    </tr>
    <tr>
      <th>541</th>
      <td>484</td>
      <td>Palkia</td>
      <td>Water</td>
      <td>Dragon</td>
      <td>790</td>
      <td>90</td>
      <td>120</td>
      <td>100</td>
      <td>150</td>
      <td>120</td>
      <td>100</td>
      <td>4</td>
      <td>True</td>
    </tr>
    <tr>
      <th>544</th>
      <td>487</td>
      <td>GiratinaAltered Forme</td>
      <td>Ghost</td>
      <td>Dragon</td>
      <td>840</td>
      <td>150</td>
      <td>100</td>
      <td>120</td>
      <td>100</td>
      <td>120</td>
      <td>90</td>
      <td>4</td>
      <td>True</td>
    </tr>
    <tr>
      <th>545</th>
      <td>487</td>
      <td>GiratinaOrigin Forme</td>
      <td>Ghost</td>
      <td>Dragon</td>
      <td>860</td>
      <td>150</td>
      <td>120</td>
      <td>100</td>
      <td>120</td>
      <td>100</td>
      <td>90</td>
      <td>4</td>
      <td>True</td>
    </tr>
    <tr>
      <th>694</th>
      <td>633</td>
      <td>Deino</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>379</td>
      <td>52</td>
      <td>65</td>
      <td>50</td>
      <td>45</td>
      <td>50</td>
      <td>38</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>695</th>
      <td>634</td>
      <td>Zweilous</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>519</td>
      <td>72</td>
      <td>85</td>
      <td>70</td>
      <td>65</td>
      <td>70</td>
      <td>58</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>696</th>
      <td>635</td>
      <td>Hydreigon</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>699</td>
      <td>92</td>
      <td>105</td>
      <td>90</td>
      <td>125</td>
      <td>90</td>
      <td>98</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>761</th>
      <td>691</td>
      <td>Dragalge</td>
      <td>Poison</td>
      <td>Dragon</td>
      <td>590</td>
      <td>65</td>
      <td>75</td>
      <td>90</td>
      <td>97</td>
      <td>123</td>
      <td>44</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>766</th>
      <td>696</td>
      <td>Tyrunt</td>
      <td>Rock</td>
      <td>Dragon</td>
      <td>461</td>
      <td>58</td>
      <td>89</td>
      <td>77</td>
      <td>45</td>
      <td>45</td>
      <td>48</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>767</th>
      <td>697</td>
      <td>Tyrantrum</td>
      <td>Rock</td>
      <td>Dragon</td>
      <td>653</td>
      <td>82</td>
      <td>121</td>
      <td>119</td>
      <td>69</td>
      <td>59</td>
      <td>71</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>790</th>
      <td>714</td>
      <td>Noibat</td>
      <td>Flying</td>
      <td>Dragon</td>
      <td>260</td>
      <td>40</td>
      <td>30</td>
      <td>35</td>
      <td>45</td>
      <td>40</td>
      <td>55</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>791</th>
      <td>715</td>
      <td>Noivern</td>
      <td>Flying</td>
      <td>Dragon</td>
      <td>567</td>
      <td>85</td>
      <td>70</td>
      <td>80</td>
      <td>97</td>
      <td>80</td>
      <td>123</td>
      <td>6</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Filtering using loc
df3 = df2.loc[(df2['Type 2'] == 'Dragon') & (df2['Type 1'] == 'Dark')]
df3
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>694</th>
      <td>633</td>
      <td>Deino</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>379</td>
      <td>52</td>
      <td>65</td>
      <td>50</td>
      <td>45</td>
      <td>50</td>
      <td>38</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>695</th>
      <td>634</td>
      <td>Zweilous</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>519</td>
      <td>72</td>
      <td>85</td>
      <td>70</td>
      <td>65</td>
      <td>70</td>
      <td>58</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>696</th>
      <td>635</td>
      <td>Hydreigon</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>699</td>
      <td>92</td>
      <td>105</td>
      <td>90</td>
      <td>125</td>
      <td>90</td>
      <td>98</td>
      <td>5</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Reset index for Dataframe df3 keeping old index column

df4 = df3.reset_index()
df4
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>694</td>
      <td>633</td>
      <td>Deino</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>379</td>
      <td>52</td>
      <td>65</td>
      <td>50</td>
      <td>45</td>
      <td>50</td>
      <td>38</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>695</td>
      <td>634</td>
      <td>Zweilous</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>519</td>
      <td>72</td>
      <td>85</td>
      <td>70</td>
      <td>65</td>
      <td>70</td>
      <td>58</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>696</td>
      <td>635</td>
      <td>Hydreigon</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>699</td>
      <td>92</td>
      <td>105</td>
      <td>90</td>
      <td>125</td>
      <td>90</td>
      <td>98</td>
      <td>5</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Reset index for Dataframe df3 removing old index column

df3.reset_index(drop=True , inplace=True)
df3
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>633</td>
      <td>Deino</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>379</td>
      <td>52</td>
      <td>65</td>
      <td>50</td>
      <td>45</td>
      <td>50</td>
      <td>38</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>634</td>
      <td>Zweilous</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>519</td>
      <td>72</td>
      <td>85</td>
      <td>70</td>
      <td>65</td>
      <td>70</td>
      <td>58</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>635</td>
      <td>Hydreigon</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>699</td>
      <td>92</td>
      <td>105</td>
      <td>90</td>
      <td>125</td>
      <td>90</td>
      <td>98</td>
      <td>5</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>447</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>596</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Fire</td>
      <td>Dragon</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>716</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



# LIKE OPERATION IN PANDAS


```python
df2.Name.str.contains("rill").head(10)
```




    0    False
    1    False
    2    False
    3    False
    4    False
    5    False
    6    False
    7    False
    8    False
    9    False
    Name: Name, dtype: bool




```python
# Display all rows containing Name "rill"
df2.loc[df2.Name.str.contains("rill")]
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>18</th>
      <td>15</td>
      <td>Beedrill</td>
      <td>Bug</td>
      <td>Poison</td>
      <td>475</td>
      <td>65</td>
      <td>90</td>
      <td>40</td>
      <td>45</td>
      <td>80</td>
      <td>75</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>19</th>
      <td>15</td>
      <td>BeedrillMega Beedrill</td>
      <td>Bug</td>
      <td>Poison</td>
      <td>565</td>
      <td>65</td>
      <td>150</td>
      <td>40</td>
      <td>15</td>
      <td>80</td>
      <td>145</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>198</th>
      <td>183</td>
      <td>Marill</td>
      <td>Water</td>
      <td>Fairy</td>
      <td>300</td>
      <td>70</td>
      <td>20</td>
      <td>50</td>
      <td>20</td>
      <td>50</td>
      <td>40</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>199</th>
      <td>184</td>
      <td>Azumarill</td>
      <td>Water</td>
      <td>Fairy</td>
      <td>520</td>
      <td>100</td>
      <td>50</td>
      <td>80</td>
      <td>60</td>
      <td>80</td>
      <td>50</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>322</th>
      <td>298</td>
      <td>Azurill</td>
      <td>Normal</td>
      <td>Fairy</td>
      <td>240</td>
      <td>50</td>
      <td>20</td>
      <td>40</td>
      <td>20</td>
      <td>40</td>
      <td>20</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>589</th>
      <td>530</td>
      <td>Excadrill</td>
      <td>Ground</td>
      <td>Steel</td>
      <td>665</td>
      <td>110</td>
      <td>135</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>88</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>653</th>
      <td>592</td>
      <td>Frillish</td>
      <td>Water</td>
      <td>Ghost</td>
      <td>390</td>
      <td>55</td>
      <td>40</td>
      <td>50</td>
      <td>65</td>
      <td>85</td>
      <td>40</td>
      <td>5</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Exclude all rows containing "rill"
df2.loc[~df2.Name.str.contains("rill")].head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>447</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>596</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Fire</td>
      <td>Dragon</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>716</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Display all rows with Type-1 as "Grass" and Type-2 as "Poison"

df2.loc[df2['Type 1'].str.contains("Grass") & df2['Type 2'].str.contains("Poison")]
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>48</th>
      <td>43</td>
      <td>Oddish</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>385</td>
      <td>45</td>
      <td>50</td>
      <td>55</td>
      <td>75</td>
      <td>65</td>
      <td>30</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49</th>
      <td>44</td>
      <td>Gloom</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>480</td>
      <td>60</td>
      <td>65</td>
      <td>70</td>
      <td>85</td>
      <td>75</td>
      <td>40</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>50</th>
      <td>45</td>
      <td>Vileplume</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>595</td>
      <td>75</td>
      <td>80</td>
      <td>85</td>
      <td>110</td>
      <td>90</td>
      <td>50</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>75</th>
      <td>69</td>
      <td>Bellsprout</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>385</td>
      <td>50</td>
      <td>75</td>
      <td>35</td>
      <td>70</td>
      <td>30</td>
      <td>40</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>76</th>
      <td>70</td>
      <td>Weepinbell</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>490</td>
      <td>65</td>
      <td>90</td>
      <td>50</td>
      <td>85</td>
      <td>45</td>
      <td>55</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>77</th>
      <td>71</td>
      <td>Victreebel</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>605</td>
      <td>80</td>
      <td>105</td>
      <td>65</td>
      <td>100</td>
      <td>70</td>
      <td>70</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>344</th>
      <td>315</td>
      <td>Roselia</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>445</td>
      <td>50</td>
      <td>60</td>
      <td>45</td>
      <td>100</td>
      <td>80</td>
      <td>65</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>451</th>
      <td>406</td>
      <td>Budew</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>295</td>
      <td>40</td>
      <td>30</td>
      <td>35</td>
      <td>50</td>
      <td>70</td>
      <td>55</td>
      <td>4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>452</th>
      <td>407</td>
      <td>Roserade</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>555</td>
      <td>60</td>
      <td>70</td>
      <td>65</td>
      <td>125</td>
      <td>105</td>
      <td>90</td>
      <td>4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>651</th>
      <td>590</td>
      <td>Foongus</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>403</td>
      <td>69</td>
      <td>55</td>
      <td>45</td>
      <td>55</td>
      <td>55</td>
      <td>15</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>652</th>
      <td>591</td>
      <td>Amoonguss</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>633</td>
      <td>114</td>
      <td>85</td>
      <td>70</td>
      <td>85</td>
      <td>80</td>
      <td>30</td>
      <td>5</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.loc[df2['Type 1'].str.contains('Grass|Water',regex = True)].head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>8</td>
      <td>Wartortle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>469</td>
      <td>59</td>
      <td>63</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>58</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>11</th>
      <td>9</td>
      <td>Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>614</td>
      <td>79</td>
      <td>83</td>
      <td>100</td>
      <td>85</td>
      <td>105</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9</td>
      <td>BlastoiseMega Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>734</td>
      <td>79</td>
      <td>103</td>
      <td>120</td>
      <td>135</td>
      <td>115</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>48</th>
      <td>43</td>
      <td>Oddish</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>385</td>
      <td>45</td>
      <td>50</td>
      <td>55</td>
      <td>75</td>
      <td>65</td>
      <td>30</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49</th>
      <td>44</td>
      <td>Gloom</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>480</td>
      <td>60</td>
      <td>65</td>
      <td>70</td>
      <td>85</td>
      <td>75</td>
      <td>40</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Due to Case-sensitive it will not return any data

df2.loc[df2['Type 1'].str.contains('grass|water',regex = True)].head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
# To ignore case we can use "case = False"

df2.loc[df2['Type 1'].str.contains('grass|water', case = False ,regex = True)].head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>8</td>
      <td>Wartortle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>469</td>
      <td>59</td>
      <td>63</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>58</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>11</th>
      <td>9</td>
      <td>Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>614</td>
      <td>79</td>
      <td>83</td>
      <td>100</td>
      <td>85</td>
      <td>105</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9</td>
      <td>BlastoiseMega Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>734</td>
      <td>79</td>
      <td>103</td>
      <td>120</td>
      <td>135</td>
      <td>115</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>48</th>
      <td>43</td>
      <td>Oddish</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>385</td>
      <td>45</td>
      <td>50</td>
      <td>55</td>
      <td>75</td>
      <td>65</td>
      <td>30</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49</th>
      <td>44</td>
      <td>Gloom</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>480</td>
      <td>60</td>
      <td>65</td>
      <td>70</td>
      <td>85</td>
      <td>75</td>
      <td>40</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# To ignore case we can use "Flags = re.I"

df2.loc[df2['Type 1'].str.contains('grass|water',flags = re.I ,regex = True)].head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>8</td>
      <td>Wartortle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>469</td>
      <td>59</td>
      <td>63</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>58</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>11</th>
      <td>9</td>
      <td>Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>614</td>
      <td>79</td>
      <td>83</td>
      <td>100</td>
      <td>85</td>
      <td>105</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9</td>
      <td>BlastoiseMega Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>734</td>
      <td>79</td>
      <td>103</td>
      <td>120</td>
      <td>135</td>
      <td>115</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>48</th>
      <td>43</td>
      <td>Oddish</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>385</td>
      <td>45</td>
      <td>50</td>
      <td>55</td>
      <td>75</td>
      <td>65</td>
      <td>30</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>49</th>
      <td>44</td>
      <td>Gloom</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>480</td>
      <td>60</td>
      <td>65</td>
      <td>70</td>
      <td>85</td>
      <td>75</td>
      <td>40</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



# Regex in Pandas dataframe


```python
#Get all rows with name starting with "wa"

df2.loc[df2.Name.str.contains('^Wa',flags = re.I ,regex = True)].head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>8</td>
      <td>Wartortle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>469</td>
      <td>59</td>
      <td>63</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>58</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>350</th>
      <td>320</td>
      <td>Wailmer</td>
      <td>Water</td>
      <td>NaN</td>
      <td>540</td>
      <td>130</td>
      <td>70</td>
      <td>35</td>
      <td>70</td>
      <td>35</td>
      <td>60</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>351</th>
      <td>321</td>
      <td>Wailord</td>
      <td>Water</td>
      <td>NaN</td>
      <td>700</td>
      <td>170</td>
      <td>90</td>
      <td>45</td>
      <td>90</td>
      <td>45</td>
      <td>60</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>400</th>
      <td>365</td>
      <td>Walrein</td>
      <td>Ice</td>
      <td>Water</td>
      <td>655</td>
      <td>110</td>
      <td>80</td>
      <td>90</td>
      <td>95</td>
      <td>90</td>
      <td>65</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>564</th>
      <td>505</td>
      <td>Watchog</td>
      <td>Normal</td>
      <td>NaN</td>
      <td>488</td>
      <td>60</td>
      <td>85</td>
      <td>69</td>
      <td>60</td>
      <td>69</td>
      <td>77</td>
      <td>5</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Get all rows with name starting with "wa" followed by any letter between a-l

df2.loc[df2.Name.str.contains('^Wa[a-l]+',flags = re.I ,regex = True)].head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>350</th>
      <td>320</td>
      <td>Wailmer</td>
      <td>Water</td>
      <td>NaN</td>
      <td>540</td>
      <td>130</td>
      <td>70</td>
      <td>35</td>
      <td>70</td>
      <td>35</td>
      <td>60</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>351</th>
      <td>321</td>
      <td>Wailord</td>
      <td>Water</td>
      <td>NaN</td>
      <td>700</td>
      <td>170</td>
      <td>90</td>
      <td>45</td>
      <td>90</td>
      <td>45</td>
      <td>60</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>400</th>
      <td>365</td>
      <td>Walrein</td>
      <td>Ice</td>
      <td>Water</td>
      <td>655</td>
      <td>110</td>
      <td>80</td>
      <td>90</td>
      <td>95</td>
      <td>90</td>
      <td>65</td>
      <td>3</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Get all rows with name starting with x , y, z

df2.loc[df2.Name.str.contains('^[x-z]',flags = re.I ,regex = True)]
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>46</th>
      <td>41</td>
      <td>Zubat</td>
      <td>Poison</td>
      <td>Flying</td>
      <td>275</td>
      <td>40</td>
      <td>45</td>
      <td>35</td>
      <td>30</td>
      <td>40</td>
      <td>55</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>157</th>
      <td>145</td>
      <td>Zapdos</td>
      <td>Electric</td>
      <td>Flying</td>
      <td>660</td>
      <td>90</td>
      <td>90</td>
      <td>85</td>
      <td>125</td>
      <td>90</td>
      <td>100</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>192</th>
      <td>178</td>
      <td>Xatu</td>
      <td>Psychic</td>
      <td>Flying</td>
      <td>515</td>
      <td>65</td>
      <td>75</td>
      <td>70</td>
      <td>95</td>
      <td>70</td>
      <td>95</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>208</th>
      <td>193</td>
      <td>Yanma</td>
      <td>Bug</td>
      <td>Flying</td>
      <td>425</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>75</td>
      <td>45</td>
      <td>95</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>286</th>
      <td>263</td>
      <td>Zigzagoon</td>
      <td>Normal</td>
      <td>NaN</td>
      <td>248</td>
      <td>38</td>
      <td>30</td>
      <td>41</td>
      <td>30</td>
      <td>41</td>
      <td>60</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>367</th>
      <td>335</td>
      <td>Zangoose</td>
      <td>Normal</td>
      <td>NaN</td>
      <td>556</td>
      <td>73</td>
      <td>115</td>
      <td>60</td>
      <td>60</td>
      <td>60</td>
      <td>90</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>520</th>
      <td>469</td>
      <td>Yanmega</td>
      <td>Bug</td>
      <td>Flying</td>
      <td>582</td>
      <td>86</td>
      <td>76</td>
      <td>86</td>
      <td>116</td>
      <td>56</td>
      <td>95</td>
      <td>4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>582</th>
      <td>523</td>
      <td>Zebstrika</td>
      <td>Electric</td>
      <td>NaN</td>
      <td>556</td>
      <td>75</td>
      <td>100</td>
      <td>63</td>
      <td>80</td>
      <td>63</td>
      <td>116</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>623</th>
      <td>562</td>
      <td>Yamask</td>
      <td>Ghost</td>
      <td>NaN</td>
      <td>341</td>
      <td>38</td>
      <td>30</td>
      <td>85</td>
      <td>55</td>
      <td>65</td>
      <td>30</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>631</th>
      <td>570</td>
      <td>Zorua</td>
      <td>Dark</td>
      <td>NaN</td>
      <td>370</td>
      <td>40</td>
      <td>65</td>
      <td>40</td>
      <td>80</td>
      <td>40</td>
      <td>65</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>632</th>
      <td>571</td>
      <td>Zoroark</td>
      <td>Dark</td>
      <td>NaN</td>
      <td>570</td>
      <td>60</td>
      <td>105</td>
      <td>60</td>
      <td>120</td>
      <td>60</td>
      <td>105</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>695</th>
      <td>634</td>
      <td>Zweilous</td>
      <td>Dark</td>
      <td>Dragon</td>
      <td>519</td>
      <td>72</td>
      <td>85</td>
      <td>70</td>
      <td>65</td>
      <td>70</td>
      <td>58</td>
      <td>5</td>
      <td>False</td>
    </tr>
    <tr>
      <th>707</th>
      <td>644</td>
      <td>Zekrom</td>
      <td>Dragon</td>
      <td>Electric</td>
      <td>840</td>
      <td>100</td>
      <td>150</td>
      <td>120</td>
      <td>120</td>
      <td>100</td>
      <td>90</td>
      <td>5</td>
      <td>True</td>
    </tr>
    <tr>
      <th>792</th>
      <td>716</td>
      <td>Xerneas</td>
      <td>Fairy</td>
      <td>NaN</td>
      <td>838</td>
      <td>126</td>
      <td>131</td>
      <td>95</td>
      <td>131</td>
      <td>98</td>
      <td>99</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>793</th>
      <td>717</td>
      <td>Yveltal</td>
      <td>Dark</td>
      <td>Flying</td>
      <td>838</td>
      <td>126</td>
      <td>131</td>
      <td>95</td>
      <td>131</td>
      <td>98</td>
      <td>99</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>794</th>
      <td>718</td>
      <td>Zygarde50% Forme</td>
      <td>Dragon</td>
      <td>Ground</td>
      <td>713</td>
      <td>108</td>
      <td>100</td>
      <td>121</td>
      <td>81</td>
      <td>95</td>
      <td>95</td>
      <td>6</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Extracting first 3 characters from "Name" column
df2['Name2'] = df2.Name.str.extract(r'(^\w{3})')
```


```python
df2.head(5)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Name2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
      <td>Bul</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
      <td>Ivy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Ven</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Ven</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Return all rows with "Name" starting with character 'B or b' 
df2.loc[df2.Name.str.match(r'(^[B|b].*)')].head(5)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Name2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
      <td>Bul</td>
    </tr>
    <tr>
      <th>11</th>
      <td>9</td>
      <td>Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>614</td>
      <td>79</td>
      <td>83</td>
      <td>100</td>
      <td>85</td>
      <td>105</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
      <td>Bla</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9</td>
      <td>BlastoiseMega Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>734</td>
      <td>79</td>
      <td>103</td>
      <td>120</td>
      <td>135</td>
      <td>115</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
      <td>Bla</td>
    </tr>
    <tr>
      <th>15</th>
      <td>12</td>
      <td>Butterfree</td>
      <td>Bug</td>
      <td>Flying</td>
      <td>430</td>
      <td>60</td>
      <td>45</td>
      <td>50</td>
      <td>90</td>
      <td>80</td>
      <td>70</td>
      <td>1</td>
      <td>False</td>
      <td>But</td>
    </tr>
    <tr>
      <th>18</th>
      <td>15</td>
      <td>Beedrill</td>
      <td>Bug</td>
      <td>Poison</td>
      <td>475</td>
      <td>65</td>
      <td>90</td>
      <td>40</td>
      <td>45</td>
      <td>80</td>
      <td>75</td>
      <td>1</td>
      <td>False</td>
      <td>Bee</td>
    </tr>
  </tbody>
</table>
</div>



# Replace values in dataframe


```python
df2.head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Name2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
      <td>Bul</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
      <td>Ivy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Ven</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Ven</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>447</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>596</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Fire</td>
      <td>Dragon</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>716</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
      <td>Squ</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2['Type 1'] = df2['Type 1'].replace({"Grass" : "Meadow" , "Fire" :"Blaze"})
```


```python
df2.head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Name2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Meadow</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
      <td>Bul</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Meadow</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
      <td>Ivy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Meadow</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Ven</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Meadow</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Ven</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>447</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Blaze</td>
      <td>Flying</td>
      <td>596</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Blaze</td>
      <td>Dragon</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Blaze</td>
      <td>Flying</td>
      <td>716</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
      <td>Squ</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2['Type 2'] = df2['Type 2'].replace({"Poison" : "Venom"})
```


```python
df2.head(5)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Name2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Meadow</td>
      <td>Venom</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
      <td>Bul</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Meadow</td>
      <td>Venom</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
      <td>Ivy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Meadow</td>
      <td>Venom</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Ven</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Meadow</td>
      <td>Venom</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Ven</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2['Type 2'] = df2['Type 2'].replace(['Venom' , 'Dragon'] , 'DANGER')
```


```python
df2.head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Name2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
      <td>Bul</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
      <td>Ivy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Ven</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Ven</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>447</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Blaze</td>
      <td>Flying</td>
      <td>596</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Blaze</td>
      <td>DANGER</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Blaze</td>
      <td>Flying</td>
      <td>716</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
      <td>Squ</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.loc[df2['Type 2'] == 'DANGER' , 'Name2'] = np.NaN
```


```python
df2.head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Name2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>447</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Blaze</td>
      <td>Flying</td>
      <td>596</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Blaze</td>
      <td>DANGER</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Blaze</td>
      <td>Flying</td>
      <td>716</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
      <td>Squ</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.loc[df2['Total'] > 400 , ['Name2' , 'Legendary']] = 'ALERT'
df2.head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Name2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>ALERT</td>
      <td>ALERT</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>ALERT</td>
      <td>ALERT</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>ALERT</td>
      <td>ALERT</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>447</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>ALERT</td>
      <td>ALERT</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Blaze</td>
      <td>Flying</td>
      <td>596</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>ALERT</td>
      <td>ALERT</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Blaze</td>
      <td>DANGER</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>ALERT</td>
      <td>ALERT</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Blaze</td>
      <td>Flying</td>
      <td>716</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>ALERT</td>
      <td>ALERT</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
      <td>Squ</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.loc[df2['Total'] > 400 , ['Legendary' , 'Name2']] = ['ALERT-1' , 'ALERT-2'] 
df2.head(10)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
      <th>Name2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>ALERT-1</td>
      <td>ALERT-2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>ALERT-1</td>
      <td>ALERT-2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Meadow</td>
      <td>DANGER</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>ALERT-1</td>
      <td>ALERT-2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
      <td>Cha</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Blaze</td>
      <td>NaN</td>
      <td>447</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>ALERT-1</td>
      <td>ALERT-2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Blaze</td>
      <td>Flying</td>
      <td>596</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>ALERT-1</td>
      <td>ALERT-2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Blaze</td>
      <td>DANGER</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>ALERT-1</td>
      <td>ALERT-2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Blaze</td>
      <td>Flying</td>
      <td>716</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>ALERT-1</td>
      <td>ALERT-2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
      <td>Squ</td>
    </tr>
  </tbody>
</table>
</div>



# Group By


```python
df = pd.read_csv('poke_updated1.csv')
df.head(5)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(['Type 1']).mean().head(10)
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
      <th>#</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
    <tr>
      <th>Type 1</th>
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
      <th>Bug</th>
      <td>334.492754</td>
      <td>445.101449</td>
      <td>56.884058</td>
      <td>70.971014</td>
      <td>70.724638</td>
      <td>53.869565</td>
      <td>64.797101</td>
      <td>61.681159</td>
      <td>3.217391</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Dark</th>
      <td>461.354839</td>
      <td>524.774194</td>
      <td>66.806452</td>
      <td>88.387097</td>
      <td>70.225806</td>
      <td>74.645161</td>
      <td>69.516129</td>
      <td>76.161290</td>
      <td>4.032258</td>
      <td>0.064516</td>
    </tr>
    <tr>
      <th>Dragon</th>
      <td>474.375000</td>
      <td>662.937500</td>
      <td>83.312500</td>
      <td>112.125000</td>
      <td>86.375000</td>
      <td>96.843750</td>
      <td>88.843750</td>
      <td>83.031250</td>
      <td>3.875000</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>Electric</th>
      <td>363.500000</td>
      <td>487.795455</td>
      <td>59.795455</td>
      <td>69.090909</td>
      <td>66.295455</td>
      <td>90.022727</td>
      <td>73.704545</td>
      <td>84.500000</td>
      <td>3.272727</td>
      <td>0.090909</td>
    </tr>
    <tr>
      <th>Fairy</th>
      <td>449.529412</td>
      <td>500.235294</td>
      <td>74.117647</td>
      <td>61.529412</td>
      <td>65.705882</td>
      <td>78.529412</td>
      <td>84.705882</td>
      <td>48.588235</td>
      <td>4.117647</td>
      <td>0.058824</td>
    </tr>
    <tr>
      <th>Fighting</th>
      <td>363.851852</td>
      <td>517.000000</td>
      <td>69.851852</td>
      <td>96.777778</td>
      <td>65.925926</td>
      <td>53.111111</td>
      <td>64.703704</td>
      <td>66.074074</td>
      <td>3.370370</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Fire</th>
      <td>327.403846</td>
      <td>538.307692</td>
      <td>69.903846</td>
      <td>84.769231</td>
      <td>67.769231</td>
      <td>88.980769</td>
      <td>72.211538</td>
      <td>74.442308</td>
      <td>3.211538</td>
      <td>0.096154</td>
    </tr>
    <tr>
      <th>Flying</th>
      <td>677.750000</td>
      <td>532.000000</td>
      <td>70.750000</td>
      <td>78.750000</td>
      <td>66.250000</td>
      <td>94.250000</td>
      <td>72.500000</td>
      <td>102.500000</td>
      <td>5.500000</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>Ghost</th>
      <td>486.500000</td>
      <td>513.437500</td>
      <td>64.437500</td>
      <td>73.781250</td>
      <td>81.187500</td>
      <td>79.343750</td>
      <td>76.468750</td>
      <td>64.343750</td>
      <td>4.187500</td>
      <td>0.062500</td>
    </tr>
    <tr>
      <th>Grass</th>
      <td>344.871429</td>
      <td>499.700000</td>
      <td>67.271429</td>
      <td>73.214286</td>
      <td>70.800000</td>
      <td>77.500000</td>
      <td>70.428571</td>
      <td>61.928571</td>
      <td>3.357143</td>
      <td>0.042857</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(['Type 1']).mean().sort_values('Attack' , ascending = False).head(10)
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
      <th>#</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
    <tr>
      <th>Type 1</th>
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
      <th>Dragon</th>
      <td>474.375000</td>
      <td>662.937500</td>
      <td>83.312500</td>
      <td>112.125000</td>
      <td>86.375000</td>
      <td>96.843750</td>
      <td>88.843750</td>
      <td>83.031250</td>
      <td>3.875000</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>Fighting</th>
      <td>363.851852</td>
      <td>517.000000</td>
      <td>69.851852</td>
      <td>96.777778</td>
      <td>65.925926</td>
      <td>53.111111</td>
      <td>64.703704</td>
      <td>66.074074</td>
      <td>3.370370</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Ground</th>
      <td>356.281250</td>
      <td>543.125000</td>
      <td>73.781250</td>
      <td>95.750000</td>
      <td>84.843750</td>
      <td>56.468750</td>
      <td>62.750000</td>
      <td>63.906250</td>
      <td>3.156250</td>
      <td>0.125000</td>
    </tr>
    <tr>
      <th>Rock</th>
      <td>392.727273</td>
      <td>556.068182</td>
      <td>65.363636</td>
      <td>92.863636</td>
      <td>100.795455</td>
      <td>63.340909</td>
      <td>75.477273</td>
      <td>55.909091</td>
      <td>3.454545</td>
      <td>0.090909</td>
    </tr>
    <tr>
      <th>Steel</th>
      <td>442.851852</td>
      <td>590.370370</td>
      <td>65.222222</td>
      <td>92.703704</td>
      <td>126.370370</td>
      <td>67.518519</td>
      <td>80.629630</td>
      <td>55.259259</td>
      <td>3.851852</td>
      <td>0.148148</td>
    </tr>
    <tr>
      <th>Dark</th>
      <td>461.354839</td>
      <td>524.774194</td>
      <td>66.806452</td>
      <td>88.387097</td>
      <td>70.225806</td>
      <td>74.645161</td>
      <td>69.516129</td>
      <td>76.161290</td>
      <td>4.032258</td>
      <td>0.064516</td>
    </tr>
    <tr>
      <th>Fire</th>
      <td>327.403846</td>
      <td>538.307692</td>
      <td>69.903846</td>
      <td>84.769231</td>
      <td>67.769231</td>
      <td>88.980769</td>
      <td>72.211538</td>
      <td>74.442308</td>
      <td>3.211538</td>
      <td>0.096154</td>
    </tr>
    <tr>
      <th>Flying</th>
      <td>677.750000</td>
      <td>532.000000</td>
      <td>70.750000</td>
      <td>78.750000</td>
      <td>66.250000</td>
      <td>94.250000</td>
      <td>72.500000</td>
      <td>102.500000</td>
      <td>5.500000</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>Poison</th>
      <td>251.785714</td>
      <td>477.500000</td>
      <td>67.250000</td>
      <td>74.678571</td>
      <td>68.821429</td>
      <td>60.428571</td>
      <td>64.392857</td>
      <td>63.571429</td>
      <td>2.535714</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Water</th>
      <td>303.089286</td>
      <td>510.705357</td>
      <td>72.062500</td>
      <td>74.151786</td>
      <td>72.946429</td>
      <td>74.812500</td>
      <td>70.517857</td>
      <td>65.964286</td>
      <td>2.857143</td>
      <td>0.035714</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(['Type 1']).mean().sort_values('Defense' , ascending = False).head(10)
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
      <th>#</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
    <tr>
      <th>Type 1</th>
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
      <th>Steel</th>
      <td>442.851852</td>
      <td>590.370370</td>
      <td>65.222222</td>
      <td>92.703704</td>
      <td>126.370370</td>
      <td>67.518519</td>
      <td>80.629630</td>
      <td>55.259259</td>
      <td>3.851852</td>
      <td>0.148148</td>
    </tr>
    <tr>
      <th>Rock</th>
      <td>392.727273</td>
      <td>556.068182</td>
      <td>65.363636</td>
      <td>92.863636</td>
      <td>100.795455</td>
      <td>63.340909</td>
      <td>75.477273</td>
      <td>55.909091</td>
      <td>3.454545</td>
      <td>0.090909</td>
    </tr>
    <tr>
      <th>Dragon</th>
      <td>474.375000</td>
      <td>662.937500</td>
      <td>83.312500</td>
      <td>112.125000</td>
      <td>86.375000</td>
      <td>96.843750</td>
      <td>88.843750</td>
      <td>83.031250</td>
      <td>3.875000</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>Ground</th>
      <td>356.281250</td>
      <td>543.125000</td>
      <td>73.781250</td>
      <td>95.750000</td>
      <td>84.843750</td>
      <td>56.468750</td>
      <td>62.750000</td>
      <td>63.906250</td>
      <td>3.156250</td>
      <td>0.125000</td>
    </tr>
    <tr>
      <th>Ghost</th>
      <td>486.500000</td>
      <td>513.437500</td>
      <td>64.437500</td>
      <td>73.781250</td>
      <td>81.187500</td>
      <td>79.343750</td>
      <td>76.468750</td>
      <td>64.343750</td>
      <td>4.187500</td>
      <td>0.062500</td>
    </tr>
    <tr>
      <th>Water</th>
      <td>303.089286</td>
      <td>510.705357</td>
      <td>72.062500</td>
      <td>74.151786</td>
      <td>72.946429</td>
      <td>74.812500</td>
      <td>70.517857</td>
      <td>65.964286</td>
      <td>2.857143</td>
      <td>0.035714</td>
    </tr>
    <tr>
      <th>Ice</th>
      <td>423.541667</td>
      <td>514.750000</td>
      <td>72.000000</td>
      <td>72.750000</td>
      <td>71.416667</td>
      <td>77.541667</td>
      <td>76.291667</td>
      <td>63.458333</td>
      <td>3.541667</td>
      <td>0.083333</td>
    </tr>
    <tr>
      <th>Grass</th>
      <td>344.871429</td>
      <td>499.700000</td>
      <td>67.271429</td>
      <td>73.214286</td>
      <td>70.800000</td>
      <td>77.500000</td>
      <td>70.428571</td>
      <td>61.928571</td>
      <td>3.357143</td>
      <td>0.042857</td>
    </tr>
    <tr>
      <th>Bug</th>
      <td>334.492754</td>
      <td>445.101449</td>
      <td>56.884058</td>
      <td>70.971014</td>
      <td>70.724638</td>
      <td>53.869565</td>
      <td>64.797101</td>
      <td>61.681159</td>
      <td>3.217391</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Dark</th>
      <td>461.354839</td>
      <td>524.774194</td>
      <td>66.806452</td>
      <td>88.387097</td>
      <td>70.225806</td>
      <td>74.645161</td>
      <td>69.516129</td>
      <td>76.161290</td>
      <td>4.032258</td>
      <td>0.064516</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby(['Type 1']).mean().sort_values('Speed' , ascending = False).head(10)
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
      <th>#</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
    <tr>
      <th>Type 1</th>
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
      <th>Flying</th>
      <td>677.750000</td>
      <td>532.000000</td>
      <td>70.750000</td>
      <td>78.750000</td>
      <td>66.250000</td>
      <td>94.250000</td>
      <td>72.500000</td>
      <td>102.500000</td>
      <td>5.500000</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>Electric</th>
      <td>363.500000</td>
      <td>487.795455</td>
      <td>59.795455</td>
      <td>69.090909</td>
      <td>66.295455</td>
      <td>90.022727</td>
      <td>73.704545</td>
      <td>84.500000</td>
      <td>3.272727</td>
      <td>0.090909</td>
    </tr>
    <tr>
      <th>Dragon</th>
      <td>474.375000</td>
      <td>662.937500</td>
      <td>83.312500</td>
      <td>112.125000</td>
      <td>86.375000</td>
      <td>96.843750</td>
      <td>88.843750</td>
      <td>83.031250</td>
      <td>3.875000</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>Psychic</th>
      <td>380.807018</td>
      <td>536.543860</td>
      <td>70.631579</td>
      <td>71.456140</td>
      <td>67.684211</td>
      <td>98.403509</td>
      <td>86.280702</td>
      <td>81.491228</td>
      <td>3.385965</td>
      <td>0.245614</td>
    </tr>
    <tr>
      <th>Dark</th>
      <td>461.354839</td>
      <td>524.774194</td>
      <td>66.806452</td>
      <td>88.387097</td>
      <td>70.225806</td>
      <td>74.645161</td>
      <td>69.516129</td>
      <td>76.161290</td>
      <td>4.032258</td>
      <td>0.064516</td>
    </tr>
    <tr>
      <th>Fire</th>
      <td>327.403846</td>
      <td>538.307692</td>
      <td>69.903846</td>
      <td>84.769231</td>
      <td>67.769231</td>
      <td>88.980769</td>
      <td>72.211538</td>
      <td>74.442308</td>
      <td>3.211538</td>
      <td>0.096154</td>
    </tr>
    <tr>
      <th>Normal</th>
      <td>319.173469</td>
      <td>480.877551</td>
      <td>77.275510</td>
      <td>73.469388</td>
      <td>59.846939</td>
      <td>55.816327</td>
      <td>63.724490</td>
      <td>71.551020</td>
      <td>3.051020</td>
      <td>0.020408</td>
    </tr>
    <tr>
      <th>Fighting</th>
      <td>363.851852</td>
      <td>517.000000</td>
      <td>69.851852</td>
      <td>96.777778</td>
      <td>65.925926</td>
      <td>53.111111</td>
      <td>64.703704</td>
      <td>66.074074</td>
      <td>3.370370</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Water</th>
      <td>303.089286</td>
      <td>510.705357</td>
      <td>72.062500</td>
      <td>74.151786</td>
      <td>72.946429</td>
      <td>74.812500</td>
      <td>70.517857</td>
      <td>65.964286</td>
      <td>2.857143</td>
      <td>0.035714</td>
    </tr>
    <tr>
      <th>Ghost</th>
      <td>486.500000</td>
      <td>513.437500</td>
      <td>64.437500</td>
      <td>73.781250</td>
      <td>81.187500</td>
      <td>79.343750</td>
      <td>76.468750</td>
      <td>64.343750</td>
      <td>4.187500</td>
      <td>0.062500</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.sum()
```




    #                                                        290251
    Name          BulbasaurIvysaurVenusaurVenusaurMega VenusaurC...
    Type 1        GrassGrassGrassGrassFireFireFireFireFireWaterW...
    Total                                                    412068
    HP                                                        55407
    Attack                                                    63201
    Defense                                                   59074
    Sp. Atk                                                   58256
    Sp. Def                                                   57522
    Speed                                                     54622
    Generation                                                 2659
    Legendary                                                    65
    dtype: object




```python
df.groupby(['Type 2']).sum().head(5)
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
      <th>#</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
    <tr>
      <th>Type 2</th>
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
      <th>Bug</th>
      <td>1146</td>
      <td>1425</td>
      <td>160</td>
      <td>270</td>
      <td>240</td>
      <td>140</td>
      <td>185</td>
      <td>185</td>
      <td>10</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Dark</th>
      <td>8277</td>
      <td>11888</td>
      <td>1511</td>
      <td>2196</td>
      <td>1441</td>
      <td>1636</td>
      <td>1397</td>
      <td>1507</td>
      <td>75</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Dragon</th>
      <td>8686</td>
      <td>11200</td>
      <td>1479</td>
      <td>1700</td>
      <td>1567</td>
      <td>1773</td>
      <td>1502</td>
      <td>1450</td>
      <td>75</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Electric</th>
      <td>2794</td>
      <td>3268</td>
      <td>529</td>
      <td>436</td>
      <td>410</td>
      <td>487</td>
      <td>441</td>
      <td>429</td>
      <td>24</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Fairy</th>
      <td>8718</td>
      <td>11101</td>
      <td>1479</td>
      <td>1417</td>
      <td>1699</td>
      <td>1725</td>
      <td>1885</td>
      <td>1408</td>
      <td>82</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.count()
```




    #             800
    Name          800
    Type 1        800
    Type 2        414
    Total         800
    HP            800
    Attack        800
    Defense       800
    Sp. Atk       800
    Sp. Def       800
    Speed         800
    Generation    800
    Legendary     800
    dtype: int64




```python
df['count1'] = 0
df.groupby(['Type 2']).count()['count1']
```




    Type 2
    Bug          3
    Dark        20
    Dragon      18
    Electric     6
    Fairy       23
    Fighting    26
    Fire        12
    Flying      97
    Ghost       14
    Grass       25
    Ground      35
    Ice         14
    Normal       4
    Poison      34
    Psychic     33
    Rock        14
    Steel       22
    Water       14
    Name: count1, dtype: int64




```python
df['count1'] = 0
df.groupby(['Type 1']).count()['count1']
```




    Type 1
    Bug          69
    Dark         31
    Dragon       32
    Electric     44
    Fairy        17
    Fighting     27
    Fire         52
    Flying        4
    Ghost        32
    Grass        70
    Ground       32
    Ice          24
    Normal       98
    Poison       28
    Psychic      57
    Rock         44
    Steel        27
    Water       112
    Name: count1, dtype: int64




```python
df['count1'] = 0
df.groupby(['Type 1' , 'Type 2' , 'Legendary']).count()['count1']
```




    Type 1  Type 2    Legendary
    Bug     Electric  False         2
            Fighting  False         2
            Fire      False         2
            Flying    False        14
            Ghost     False         1
                                   ..
    Water   Ice       False         3
            Poison    False         3
            Psychic   False         5
            Rock      False         4
            Steel     False         1
    Name: count1, Length: 150, dtype: int64



# Loading Data in Chunks


```python
for df in pd.read_csv('poke_updated1.csv', chunksize=10):
    print(df)
```

       #                       Name Type 1  ... Speed  Generation  Legendary
    0  1                  Bulbasaur  Grass  ...    45           1      False
    1  2                    Ivysaur  Grass  ...    60           1      False
    2  3                   Venusaur  Grass  ...    80           1      False
    3  3      VenusaurMega Venusaur  Grass  ...    80           1      False
    4  4                 Charmander   Fire  ...    65           1      False
    5  5                 Charmeleon   Fire  ...    80           1      False
    6  6                  Charizard   Fire  ...   100           1      False
    7  6  CharizardMega Charizard X   Fire  ...   100           1      False
    8  6  CharizardMega Charizard Y   Fire  ...   100           1      False
    9  7                   Squirtle  Water  ...    43           1      False
    
    [10 rows x 13 columns]
         #                     Name Type 1  ... Speed  Generation  Legendary
    10   8                Wartortle  Water  ...    58           1      False
    11   9                Blastoise  Water  ...    78           1      False
    12   9  BlastoiseMega Blastoise  Water  ...    78           1      False
    13  10                 Caterpie    Bug  ...    45           1      False
    14  11                  Metapod    Bug  ...    30           1      False
    15  12               Butterfree    Bug  ...    70           1      False
    16  13                   Weedle    Bug  ...    50           1      False
    17  14                   Kakuna    Bug  ...    35           1      False
    18  15                 Beedrill    Bug  ...    75           1      False
    19  15    BeedrillMega Beedrill    Bug  ...   145           1      False
    
    [10 rows x 13 columns]
         #                 Name  Type 1  ... Speed  Generation  Legendary
    20  16               Pidgey  Normal  ...    56           1      False
    21  17            Pidgeotto  Normal  ...    71           1      False
    22  18              Pidgeot  Normal  ...   101           1      False
    23  18  PidgeotMega Pidgeot  Normal  ...   121           1      False
    24  19              Rattata  Normal  ...    72           1      False
    25  20             Raticate  Normal  ...    97           1      False
    26  21              Spearow  Normal  ...    70           1      False
    27  22               Fearow  Normal  ...   100           1      False
    28  23                Ekans  Poison  ...    55           1      False
    29  24                Arbok  Poison  ...    80           1      False
    
    [10 rows x 13 columns]
         #       Name    Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    30  25    Pikachu  Electric     NaN  ...       50     90           1      False
    31  26     Raichu  Electric     NaN  ...       80    110           1      False
    32  27  Sandshrew    Ground     NaN  ...       30     40           1      False
    33  28  Sandslash    Ground     NaN  ...       55     65           1      False
    34  29   Nidoran♀    Poison     NaN  ...       40     41           1      False
    35  30   Nidorina    Poison     NaN  ...       55     56           1      False
    36  31  Nidoqueen    Poison  Ground  ...       85     76           1      False
    37  32   Nidoran♂    Poison     NaN  ...       40     50           1      False
    38  33   Nidorino    Poison     NaN  ...       55     65           1      False
    39  34   Nidoking    Poison  Ground  ...       75     85           1      False
    
    [10 rows x 13 columns]
         #        Name  Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    40  35    Clefairy   Fairy     NaN  ...       65     35           1      False
    41  36    Clefable   Fairy     NaN  ...       90     60           1      False
    42  37      Vulpix    Fire     NaN  ...       65     65           1      False
    43  38   Ninetales    Fire     NaN  ...      100    100           1      False
    44  39  Jigglypuff  Normal   Fairy  ...       25     20           1      False
    45  40  Wigglytuff  Normal   Fairy  ...       50     45           1      False
    46  41       Zubat  Poison  Flying  ...       40     55           1      False
    47  42      Golbat  Poison  Flying  ...       75     90           1      False
    48  43      Oddish   Grass  Poison  ...       65     30           1      False
    49  44       Gloom   Grass  Poison  ...       75     40           1      False
    
    [10 rows x 13 columns]
         #       Name  Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    50  45  Vileplume   Grass  Poison  ...       90     50           1      False
    51  46      Paras     Bug   Grass  ...       55     25           1      False
    52  47   Parasect     Bug   Grass  ...       80     30           1      False
    53  48    Venonat     Bug  Poison  ...       55     45           1      False
    54  49   Venomoth     Bug  Poison  ...       75     90           1      False
    55  50    Diglett  Ground     NaN  ...       45     95           1      False
    56  51    Dugtrio  Ground     NaN  ...       70    120           1      False
    57  52     Meowth  Normal     NaN  ...       40     90           1      False
    58  53    Persian  Normal     NaN  ...       65    115           1      False
    59  54    Psyduck   Water     NaN  ...       50     55           1      False
    
    [10 rows x 13 columns]
         #       Name    Type 1    Type 2  ...  Sp. Def  Speed  Generation  Legendary
    60  55    Golduck     Water       NaN  ...       80     85           1      False
    61  56     Mankey  Fighting       NaN  ...       45     70           1      False
    62  57   Primeape  Fighting       NaN  ...       70     95           1      False
    63  58  Growlithe      Fire       NaN  ...       50     60           1      False
    64  59   Arcanine      Fire       NaN  ...       80     95           1      False
    65  60    Poliwag     Water       NaN  ...       40     90           1      False
    66  61  Poliwhirl     Water       NaN  ...       50     90           1      False
    67  62  Poliwrath     Water  Fighting  ...       90     70           1      False
    68  63       Abra   Psychic       NaN  ...       55     90           1      False
    69  64    Kadabra   Psychic       NaN  ...       70    105           1      False
    
    [10 rows x 13 columns]
         #                   Name    Type 1  ... Speed  Generation  Legendary
    70  65               Alakazam   Psychic  ...   120           1      False
    71  65  AlakazamMega Alakazam   Psychic  ...   150           1      False
    72  66                 Machop  Fighting  ...    35           1      False
    73  67                Machoke  Fighting  ...    45           1      False
    74  68                Machamp  Fighting  ...    55           1      False
    75  69             Bellsprout     Grass  ...    40           1      False
    76  70             Weepinbell     Grass  ...    55           1      False
    77  71             Victreebel     Grass  ...    70           1      False
    78  72              Tentacool     Water  ...    70           1      False
    79  73             Tentacruel     Water  ...   100           1      False
    
    [10 rows x 13 columns]
         #                 Name    Type 1  ... Speed  Generation  Legendary
    80  74              Geodude      Rock  ...    20           1      False
    81  75             Graveler      Rock  ...    35           1      False
    82  76                Golem      Rock  ...    45           1      False
    83  77               Ponyta      Fire  ...    90           1      False
    84  78             Rapidash      Fire  ...   105           1      False
    85  79             Slowpoke     Water  ...    15           1      False
    86  80              Slowbro     Water  ...    30           1      False
    87  80  SlowbroMega Slowbro     Water  ...    30           1      False
    88  81            Magnemite  Electric  ...    45           1      False
    89  82             Magneton  Electric  ...    70           1      False
    
    [10 rows x 13 columns]
         #        Name  Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    90  83  Farfetch'd  Normal  Flying  ...       62     60           1      False
    91  84       Doduo  Normal  Flying  ...       35     75           1      False
    92  85      Dodrio  Normal  Flying  ...       60    100           1      False
    93  86        Seel   Water     NaN  ...       70     45           1      False
    94  87     Dewgong   Water     Ice  ...       95     70           1      False
    95  88      Grimer  Poison     NaN  ...       50     25           1      False
    96  89         Muk  Poison     NaN  ...      100     50           1      False
    97  90    Shellder   Water     NaN  ...       25     40           1      False
    98  91    Cloyster   Water     Ice  ...       45     70           1      False
    99  92      Gastly   Ghost  Poison  ...       35     80           1      False
    
    [10 rows x 13 columns]
           #               Name    Type 1  ... Speed  Generation  Legendary
    100   93            Haunter     Ghost  ...    95           1      False
    101   94             Gengar     Ghost  ...   110           1      False
    102   94  GengarMega Gengar     Ghost  ...   130           1      False
    103   95               Onix      Rock  ...    70           1      False
    104   96            Drowzee   Psychic  ...    42           1      False
    105   97              Hypno   Psychic  ...    67           1      False
    106   98             Krabby     Water  ...    50           1      False
    107   99            Kingler     Water  ...    75           1      False
    108  100            Voltorb  Electric  ...   100           1      False
    109  101          Electrode  Electric  ...   140           1      False
    
    [10 rows x 13 columns]
           #        Name    Type 1   Type 2  ...  Sp. Def  Speed  Generation  Legendary
    110  102   Exeggcute     Grass  Psychic  ...       45     40           1      False
    111  103   Exeggutor     Grass  Psychic  ...       65     55           1      False
    112  104      Cubone    Ground      NaN  ...       50     35           1      False
    113  105     Marowak    Ground      NaN  ...       80     45           1      False
    114  106   Hitmonlee  Fighting      NaN  ...      110     87           1      False
    115  107  Hitmonchan  Fighting      NaN  ...      110     76           1      False
    116  108   Lickitung    Normal      NaN  ...       75     30           1      False
    117  109     Koffing    Poison      NaN  ...       45     35           1      False
    118  110     Weezing    Poison      NaN  ...       70     60           1      False
    119  111     Rhyhorn    Ground     Rock  ...       30     25           1      False
    
    [10 rows x 13 columns]
           #                       Name  Type 1  ... Speed  Generation  Legendary
    120  112                     Rhydon  Ground  ...    40           1      False
    121  113                    Chansey  Normal  ...    50           1      False
    122  114                    Tangela   Grass  ...    60           1      False
    123  115                 Kangaskhan  Normal  ...    90           1      False
    124  115  KangaskhanMega Kangaskhan  Normal  ...   100           1      False
    125  116                     Horsea   Water  ...    60           1      False
    126  117                     Seadra   Water  ...    85           1      False
    127  118                    Goldeen   Water  ...    63           1      False
    128  119                    Seaking   Water  ...    68           1      False
    129  120                     Staryu   Water  ...    85           1      False
    
    [10 rows x 13 columns]
           #               Name    Type 1  ... Speed  Generation  Legendary
    130  121            Starmie     Water  ...   115           1      False
    131  122           Mr. Mime   Psychic  ...    90           1      False
    132  123            Scyther       Bug  ...   105           1      False
    133  124               Jynx       Ice  ...    95           1      False
    134  125         Electabuzz  Electric  ...   105           1      False
    135  126             Magmar      Fire  ...    93           1      False
    136  127             Pinsir       Bug  ...    85           1      False
    137  127  PinsirMega Pinsir       Bug  ...   105           1      False
    138  128             Tauros    Normal  ...   110           1      False
    139  129           Magikarp     Water  ...    80           1      False
    
    [10 rows x 13 columns]
           #                   Name    Type 1  ... Speed  Generation  Legendary
    140  130               Gyarados     Water  ...    81           1      False
    141  130  GyaradosMega Gyarados     Water  ...    81           1      False
    142  131                 Lapras     Water  ...    60           1      False
    143  132                  Ditto    Normal  ...    48           1      False
    144  133                  Eevee    Normal  ...    55           1      False
    145  134               Vaporeon     Water  ...    65           1      False
    146  135                Jolteon  Electric  ...   130           1      False
    147  136                Flareon      Fire  ...    65           1      False
    148  137                Porygon    Normal  ...    40           1      False
    149  138                Omanyte      Rock  ...    35           1      False
    
    [10 rows x 13 columns]
           #                       Name    Type 1  ... Speed  Generation  Legendary
    150  139                    Omastar      Rock  ...    55           1      False
    151  140                     Kabuto      Rock  ...    55           1      False
    152  141                   Kabutops      Rock  ...    80           1      False
    153  142                 Aerodactyl      Rock  ...   130           1      False
    154  142  AerodactylMega Aerodactyl      Rock  ...   150           1      False
    155  143                    Snorlax    Normal  ...    30           1      False
    156  144                   Articuno       Ice  ...    85           1       True
    157  145                     Zapdos  Electric  ...   100           1       True
    158  146                    Moltres      Fire  ...    90           1       True
    159  147                    Dratini    Dragon  ...    50           1      False
    
    [10 rows x 13 columns]
           #                 Name   Type 1  ... Speed  Generation  Legendary
    160  148            Dragonair   Dragon  ...    70           1      False
    161  149            Dragonite   Dragon  ...    80           1      False
    162  150               Mewtwo  Psychic  ...   130           1       True
    163  150  MewtwoMega Mewtwo X  Psychic  ...   130           1       True
    164  150  MewtwoMega Mewtwo Y  Psychic  ...   140           1       True
    165  151                  Mew  Psychic  ...   100           1      False
    166  152            Chikorita    Grass  ...    45           2      False
    167  153              Bayleef    Grass  ...    60           2      False
    168  154             Meganium    Grass  ...    80           2      False
    169  155            Cyndaquil     Fire  ...    65           2      False
    
    [10 rows x 13 columns]
           #        Name  Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    170  156     Quilava    Fire     NaN  ...       65     80           2      False
    171  157  Typhlosion    Fire     NaN  ...       85    100           2      False
    172  158    Totodile   Water     NaN  ...       48     43           2      False
    173  159    Croconaw   Water     NaN  ...       63     58           2      False
    174  160  Feraligatr   Water     NaN  ...       83     78           2      False
    175  161     Sentret  Normal     NaN  ...       45     20           2      False
    176  162      Furret  Normal     NaN  ...       55     90           2      False
    177  163    Hoothoot  Normal  Flying  ...       56     50           2      False
    178  164     Noctowl  Normal  Flying  ...       96     70           2      False
    179  165      Ledyba     Bug  Flying  ...       80     55           2      False
    
    [10 rows x 13 columns]
           #       Name    Type 1    Type 2  ...  Sp. Def  Speed  Generation  Legendary
    180  166     Ledian       Bug    Flying  ...      110     85           2      False
    181  167   Spinarak       Bug    Poison  ...       40     30           2      False
    182  168    Ariados       Bug    Poison  ...       60     40           2      False
    183  169     Crobat    Poison    Flying  ...       80    130           2      False
    184  170   Chinchou     Water  Electric  ...       56     67           2      False
    185  171    Lanturn     Water  Electric  ...       76     67           2      False
    186  172      Pichu  Electric       NaN  ...       35     60           2      False
    187  173     Cleffa     Fairy       NaN  ...       55     15           2      False
    188  174  Igglybuff    Normal     Fairy  ...       20     15           2      False
    189  175     Togepi     Fairy       NaN  ...       65     20           2      False
    
    [10 rows x 13 columns]
           #                   Name    Type 1  ... Speed  Generation  Legendary
    190  176                Togetic     Fairy  ...    40           2      False
    191  177                   Natu   Psychic  ...    70           2      False
    192  178                   Xatu   Psychic  ...    95           2      False
    193  179                 Mareep  Electric  ...    35           2      False
    194  180                Flaaffy  Electric  ...    45           2      False
    195  181               Ampharos  Electric  ...    55           2      False
    196  181  AmpharosMega Ampharos  Electric  ...    45           2      False
    197  182              Bellossom     Grass  ...    50           2      False
    198  183                 Marill     Water  ...    40           2      False
    199  184              Azumarill     Water  ...    50           2      False
    
    [10 rows x 13 columns]
           #       Name  Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    200  185  Sudowoodo    Rock     NaN  ...       65     30           2      False
    201  186   Politoed   Water     NaN  ...      100     70           2      False
    202  187     Hoppip   Grass  Flying  ...       55     50           2      False
    203  188   Skiploom   Grass  Flying  ...       65     80           2      False
    204  189   Jumpluff   Grass  Flying  ...       95    110           2      False
    205  190      Aipom  Normal     NaN  ...       55     85           2      False
    206  191    Sunkern   Grass     NaN  ...       30     30           2      False
    207  192   Sunflora   Grass     NaN  ...       85     30           2      False
    208  193      Yanma     Bug  Flying  ...       45     95           2      False
    209  194     Wooper   Water  Ground  ...       25     15           2      False
    
    [10 rows x 13 columns]
           #        Name   Type 1   Type 2  ...  Sp. Def  Speed  Generation  Legendary
    210  195    Quagsire    Water   Ground  ...       65     35           2      False
    211  196      Espeon  Psychic      NaN  ...       95    110           2      False
    212  197     Umbreon     Dark      NaN  ...      130     65           2      False
    213  198     Murkrow     Dark   Flying  ...       42     91           2      False
    214  199    Slowking    Water  Psychic  ...      110     30           2      False
    215  200  Misdreavus    Ghost      NaN  ...       85     85           2      False
    216  201       Unown  Psychic      NaN  ...       48     48           2      False
    217  202   Wobbuffet  Psychic      NaN  ...       58     33           2      False
    218  203   Girafarig   Normal  Psychic  ...       65     85           2      False
    219  204      Pineco      Bug      NaN  ...       35     15           2      False
    
    [10 rows x 13 columns]
           #                 Name  Type 1  ... Speed  Generation  Legendary
    220  205           Forretress     Bug  ...    40           2      False
    221  206            Dunsparce  Normal  ...    45           2      False
    222  207               Gligar  Ground  ...    85           2      False
    223  208              Steelix   Steel  ...    30           2      False
    224  208  SteelixMega Steelix   Steel  ...    30           2      False
    225  209             Snubbull   Fairy  ...    30           2      False
    226  210             Granbull   Fairy  ...    45           2      False
    227  211             Qwilfish   Water  ...    85           2      False
    228  212               Scizor     Bug  ...    65           2      False
    229  212    ScizorMega Scizor     Bug  ...    75           2      False
    
    [10 rows x 13 columns]
           #                     Name  Type 1  ... Speed  Generation  Legendary
    230  213                  Shuckle     Bug  ...     5           2      False
    231  214                Heracross     Bug  ...    85           2      False
    232  214  HeracrossMega Heracross     Bug  ...    75           2      False
    233  215                  Sneasel    Dark  ...   115           2      False
    234  216                Teddiursa  Normal  ...    40           2      False
    235  217                 Ursaring  Normal  ...    55           2      False
    236  218                   Slugma    Fire  ...    20           2      False
    237  219                 Magcargo    Fire  ...    30           2      False
    238  220                   Swinub     Ice  ...    50           2      False
    239  221                Piloswine     Ice  ...    50           2      False
    
    [10 rows x 13 columns]
           #                   Name Type 1  ... Speed  Generation  Legendary
    240  222                Corsola  Water  ...    35           2      False
    241  223               Remoraid  Water  ...    65           2      False
    242  224              Octillery  Water  ...    45           2      False
    243  225               Delibird    Ice  ...    75           2      False
    244  226                Mantine  Water  ...    70           2      False
    245  227               Skarmory  Steel  ...    70           2      False
    246  228               Houndour   Dark  ...    65           2      False
    247  229               Houndoom   Dark  ...    95           2      False
    248  229  HoundoomMega Houndoom   Dark  ...   115           2      False
    249  230                Kingdra  Water  ...    85           2      False
    
    [10 rows x 13 columns]
           #       Name    Type 1   Type 2  ...  Sp. Def  Speed  Generation  Legendary
    250  231     Phanpy    Ground      NaN  ...       40     40           2      False
    251  232    Donphan    Ground      NaN  ...       60     50           2      False
    252  233   Porygon2    Normal      NaN  ...       95     60           2      False
    253  234   Stantler    Normal      NaN  ...       65     85           2      False
    254  235   Smeargle    Normal      NaN  ...       45     75           2      False
    255  236    Tyrogue  Fighting      NaN  ...       35     35           2      False
    256  237  Hitmontop  Fighting      NaN  ...      110     70           2      False
    257  238   Smoochum       Ice  Psychic  ...       65     65           2      False
    258  239     Elekid  Electric      NaN  ...       55     95           2      False
    259  240      Magby      Fire      NaN  ...       55     83           2      False
    
    [10 rows x 13 columns]
           #                     Name    Type 1  ... Speed  Generation  Legendary
    260  241                  Miltank    Normal  ...   100           2      False
    261  242                  Blissey    Normal  ...    55           2      False
    262  243                   Raikou  Electric  ...   115           2       True
    263  244                    Entei      Fire  ...   100           2       True
    264  245                  Suicune     Water  ...    85           2       True
    265  246                 Larvitar      Rock  ...    41           2      False
    266  247                  Pupitar      Rock  ...    51           2      False
    267  248                Tyranitar      Rock  ...    61           2      False
    268  248  TyranitarMega Tyranitar      Rock  ...    71           2      False
    269  249                    Lugia   Psychic  ...   110           2       True
    
    [10 rows x 13 columns]
           #                   Name   Type 1  ... Speed  Generation  Legendary
    270  250                  Ho-oh     Fire  ...    90           2       True
    271  251                 Celebi  Psychic  ...   100           2      False
    272  252                Treecko    Grass  ...    70           3      False
    273  253                Grovyle    Grass  ...    95           3      False
    274  254               Sceptile    Grass  ...   120           3      False
    275  254  SceptileMega Sceptile    Grass  ...   145           3      False
    276  255                Torchic     Fire  ...    45           3      False
    277  256              Combusken     Fire  ...    55           3      False
    278  257               Blaziken     Fire  ...    80           3      False
    279  257  BlazikenMega Blaziken     Fire  ...   100           3      False
    
    [10 rows x 13 columns]
           #                   Name  Type 1  ... Speed  Generation  Legendary
    280  258                 Mudkip   Water  ...    40           3      False
    281  259              Marshtomp   Water  ...    50           3      False
    282  260               Swampert   Water  ...    60           3      False
    283  260  SwampertMega Swampert   Water  ...    70           3      False
    284  261              Poochyena    Dark  ...    35           3      False
    285  262              Mightyena    Dark  ...    70           3      False
    286  263              Zigzagoon  Normal  ...    60           3      False
    287  264                Linoone  Normal  ...   100           3      False
    288  265                Wurmple     Bug  ...    20           3      False
    289  266                Silcoon     Bug  ...    15           3      False
    
    [10 rows x 13 columns]
           #       Name  Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    290  267  Beautifly     Bug  Flying  ...       50     65           3      False
    291  268    Cascoon     Bug     NaN  ...       25     15           3      False
    292  269     Dustox     Bug  Poison  ...       90     65           3      False
    293  270      Lotad   Water   Grass  ...       50     30           3      False
    294  271     Lombre   Water   Grass  ...       70     50           3      False
    295  272   Ludicolo   Water   Grass  ...      100     70           3      False
    296  273     Seedot   Grass     NaN  ...       30     30           3      False
    297  274    Nuzleaf   Grass    Dark  ...       40     60           3      False
    298  275    Shiftry   Grass    Dark  ...       60     80           3      False
    299  276    Taillow  Normal  Flying  ...       30     85           3      False
    
    [10 rows x 13 columns]
           #                     Name   Type 1  ... Speed  Generation  Legendary
    300  277                  Swellow   Normal  ...   125           3      False
    301  278                  Wingull    Water  ...    85           3      False
    302  279                 Pelipper    Water  ...    65           3      False
    303  280                    Ralts  Psychic  ...    40           3      False
    304  281                   Kirlia  Psychic  ...    50           3      False
    305  282                Gardevoir  Psychic  ...    80           3      False
    306  282  GardevoirMega Gardevoir  Psychic  ...   100           3      False
    307  283                  Surskit      Bug  ...    65           3      False
    308  284               Masquerain      Bug  ...    60           3      False
    309  285                Shroomish    Grass  ...    35           3      False
    
    [10 rows x 13 columns]
           #      Name  Type 1    Type 2  ...  Sp. Def  Speed  Generation  Legendary
    310  286   Breloom   Grass  Fighting  ...       60     70           3      False
    311  287   Slakoth  Normal       NaN  ...       35     30           3      False
    312  288  Vigoroth  Normal       NaN  ...       55     90           3      False
    313  289   Slaking  Normal       NaN  ...       65    100           3      False
    314  290   Nincada     Bug    Ground  ...       30     40           3      False
    315  291   Ninjask     Bug    Flying  ...       50    160           3      False
    316  292  Shedinja     Bug     Ghost  ...       30     40           3      False
    317  293   Whismur  Normal       NaN  ...       23     28           3      False
    318  294   Loudred  Normal       NaN  ...       43     48           3      False
    319  295   Exploud  Normal       NaN  ...       73     68           3      False
    
    [10 rows x 13 columns]
           #                 Name    Type 1  ... Speed  Generation  Legendary
    320  296             Makuhita  Fighting  ...    25           3      False
    321  297             Hariyama  Fighting  ...    50           3      False
    322  298              Azurill    Normal  ...    20           3      False
    323  299             Nosepass      Rock  ...    30           3      False
    324  300               Skitty    Normal  ...    50           3      False
    325  301             Delcatty    Normal  ...    70           3      False
    326  302              Sableye      Dark  ...    50           3      False
    327  302  SableyeMega Sableye      Dark  ...    20           3      False
    328  303               Mawile     Steel  ...    50           3      False
    329  303    MawileMega Mawile     Steel  ...    50           3      False
    
    [10 rows x 13 columns]
           #                     Name    Type 1  ... Speed  Generation  Legendary
    330  304                     Aron     Steel  ...    30           3      False
    331  305                   Lairon     Steel  ...    40           3      False
    332  306                   Aggron     Steel  ...    50           3      False
    333  306        AggronMega Aggron     Steel  ...    50           3      False
    334  307                 Meditite  Fighting  ...    60           3      False
    335  308                 Medicham  Fighting  ...    80           3      False
    336  308    MedichamMega Medicham  Fighting  ...   100           3      False
    337  309                Electrike  Electric  ...    65           3      False
    338  310                Manectric  Electric  ...   105           3      False
    339  310  ManectricMega Manectric  Electric  ...   135           3      False
    
    [10 rows x 13 columns]
           #                   Name    Type 1  ... Speed  Generation  Legendary
    340  311                 Plusle  Electric  ...    95           3      False
    341  312                  Minun  Electric  ...    95           3      False
    342  313                Volbeat       Bug  ...    85           3      False
    343  314               Illumise       Bug  ...    85           3      False
    344  315                Roselia     Grass  ...    65           3      False
    345  316                 Gulpin    Poison  ...    40           3      False
    346  317                 Swalot    Poison  ...    55           3      False
    347  318               Carvanha     Water  ...    65           3      False
    348  319               Sharpedo     Water  ...    95           3      False
    349  319  SharpedoMega Sharpedo     Water  ...   105           3      False
    
    [10 rows x 13 columns]
           #                   Name   Type 1  ... Speed  Generation  Legendary
    350  320                Wailmer    Water  ...    60           3      False
    351  321                Wailord    Water  ...    60           3      False
    352  322                  Numel     Fire  ...    35           3      False
    353  323               Camerupt     Fire  ...    40           3      False
    354  323  CameruptMega Camerupt     Fire  ...    20           3      False
    355  324                Torkoal     Fire  ...    20           3      False
    356  325                 Spoink  Psychic  ...    60           3      False
    357  326                Grumpig  Psychic  ...    80           3      False
    358  327                 Spinda   Normal  ...    60           3      False
    359  328               Trapinch   Ground  ...    10           3      False
    
    [10 rows x 13 columns]
           #                 Name  Type 1  ... Speed  Generation  Legendary
    360  329              Vibrava  Ground  ...    70           3      False
    361  330               Flygon  Ground  ...   100           3      False
    362  331               Cacnea   Grass  ...    35           3      False
    363  332             Cacturne   Grass  ...    55           3      False
    364  333               Swablu  Normal  ...    50           3      False
    365  334              Altaria  Dragon  ...    80           3      False
    366  334  AltariaMega Altaria  Dragon  ...    80           3      False
    367  335             Zangoose  Normal  ...    90           3      False
    368  336              Seviper  Poison  ...    65           3      False
    369  337             Lunatone    Rock  ...    70           3      False
    
    [10 rows x 13 columns]
           #       Name  Type 1   Type 2  ...  Sp. Def  Speed  Generation  Legendary
    370  338    Solrock    Rock  Psychic  ...       65     70           3      False
    371  339   Barboach   Water   Ground  ...       41     60           3      False
    372  340   Whiscash   Water   Ground  ...       71     60           3      False
    373  341   Corphish   Water      NaN  ...       35     35           3      False
    374  342  Crawdaunt   Water     Dark  ...       55     55           3      False
    375  343     Baltoy  Ground  Psychic  ...       70     55           3      False
    376  344    Claydol  Ground  Psychic  ...      120     75           3      False
    377  345     Lileep    Rock    Grass  ...       87     23           3      False
    378  346    Cradily    Rock    Grass  ...      107     43           3      False
    379  347    Anorith    Rock      Bug  ...       50     75           3      False
    
    [10 rows x 13 columns]
           #                 Name  Type 1  ... Speed  Generation  Legendary
    380  348              Armaldo    Rock  ...    45           3      False
    381  349               Feebas   Water  ...    80           3      False
    382  350              Milotic   Water  ...    81           3      False
    383  351             Castform  Normal  ...    70           3      False
    384  352              Kecleon  Normal  ...    40           3      False
    385  353              Shuppet   Ghost  ...    45           3      False
    386  354              Banette   Ghost  ...    65           3      False
    387  354  BanetteMega Banette   Ghost  ...    75           3      False
    388  355              Duskull   Ghost  ...    25           3      False
    389  356             Dusclops   Ghost  ...    25           3      False
    
    [10 rows x 13 columns]
           #               Name   Type 1  ... Speed  Generation  Legendary
    390  357            Tropius    Grass  ...    51           3      False
    391  358           Chimecho  Psychic  ...    65           3      False
    392  359              Absol     Dark  ...    75           3      False
    393  359    AbsolMega Absol     Dark  ...   115           3      False
    394  360             Wynaut  Psychic  ...    23           3      False
    395  361            Snorunt      Ice  ...    50           3      False
    396  362             Glalie      Ice  ...    80           3      False
    397  362  GlalieMega Glalie      Ice  ...   100           3      False
    398  363             Spheal      Ice  ...    25           3      False
    399  364             Sealeo      Ice  ...    45           3      False
    
    [10 rows x 13 columns]
           #                     Name  Type 1  ... Speed  Generation  Legendary
    400  365                  Walrein     Ice  ...    65           3      False
    401  366                 Clamperl   Water  ...    32           3      False
    402  367                  Huntail   Water  ...    52           3      False
    403  368                 Gorebyss   Water  ...    52           3      False
    404  369                Relicanth   Water  ...    55           3      False
    405  370                  Luvdisc   Water  ...    97           3      False
    406  371                    Bagon  Dragon  ...    50           3      False
    407  372                  Shelgon  Dragon  ...    50           3      False
    408  373                Salamence  Dragon  ...   100           3      False
    409  373  SalamenceMega Salamence  Dragon  ...   120           3      False
    
    [10 rows x 13 columns]
           #                     Name  Type 1  ... Speed  Generation  Legendary
    410  374                   Beldum   Steel  ...    30           3      False
    411  375                   Metang   Steel  ...    50           3      False
    412  376                Metagross   Steel  ...    70           3      False
    413  376  MetagrossMega Metagross   Steel  ...   110           3      False
    414  377                 Regirock    Rock  ...    50           3       True
    415  378                   Regice     Ice  ...    50           3       True
    416  379                Registeel   Steel  ...    50           3       True
    417  380                   Latias  Dragon  ...   110           3       True
    418  380        LatiasMega Latias  Dragon  ...   110           3       True
    419  381                   Latios  Dragon  ...   110           3       True
    
    [10 rows x 13 columns]
           #                   Name   Type 1  ... Speed  Generation  Legendary
    420  381      LatiosMega Latios   Dragon  ...   110           3       True
    421  382                 Kyogre    Water  ...    90           3       True
    422  382    KyogrePrimal Kyogre    Water  ...    90           3       True
    423  383                Groudon   Ground  ...    90           3       True
    424  383  GroudonPrimal Groudon   Ground  ...    90           3       True
    425  384               Rayquaza   Dragon  ...    95           3       True
    426  384  RayquazaMega Rayquaza   Dragon  ...   115           3       True
    427  385                Jirachi    Steel  ...   100           3       True
    428  386     DeoxysNormal Forme  Psychic  ...   150           3       True
    429  386     DeoxysAttack Forme  Psychic  ...   150           3       True
    
    [10 rows x 13 columns]
           #                 Name   Type 1  ... Speed  Generation  Legendary
    430  386  DeoxysDefense Forme  Psychic  ...    90           3       True
    431  386    DeoxysSpeed Forme  Psychic  ...   180           3       True
    432  387              Turtwig    Grass  ...    31           4      False
    433  388               Grotle    Grass  ...    36           4      False
    434  389             Torterra    Grass  ...    56           4      False
    435  390             Chimchar     Fire  ...    61           4      False
    436  391             Monferno     Fire  ...    81           4      False
    437  392            Infernape     Fire  ...   108           4      False
    438  393               Piplup    Water  ...    40           4      False
    439  394             Prinplup    Water  ...    50           4      False
    
    [10 rows x 13 columns]
           #        Name    Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    440  395    Empoleon     Water   Steel  ...      101     60           4      False
    441  396      Starly    Normal  Flying  ...       30     60           4      False
    442  397    Staravia    Normal  Flying  ...       40     80           4      False
    443  398   Staraptor    Normal  Flying  ...       60    100           4      False
    444  399      Bidoof    Normal     NaN  ...       40     31           4      False
    445  400     Bibarel    Normal   Water  ...       60     71           4      False
    446  401   Kricketot       Bug     NaN  ...       41     25           4      False
    447  402  Kricketune       Bug     NaN  ...       51     65           4      False
    448  403       Shinx  Electric     NaN  ...       34     45           4      False
    449  404       Luxio  Electric     NaN  ...       49     60           4      False
    
    [10 rows x 13 columns]
           #                 Name    Type 1  ... Speed  Generation  Legendary
    450  405               Luxray  Electric  ...    70           4      False
    451  406                Budew     Grass  ...    55           4      False
    452  407             Roserade     Grass  ...    90           4      False
    453  408             Cranidos      Rock  ...    58           4      False
    454  409            Rampardos      Rock  ...    58           4      False
    455  410             Shieldon      Rock  ...    30           4      False
    456  411            Bastiodon      Rock  ...    30           4      False
    457  412                Burmy       Bug  ...    36           4      False
    458  413  WormadamPlant Cloak       Bug  ...    36           4      False
    459  413  WormadamSandy Cloak       Bug  ...    36           4      False
    
    [10 rows x 13 columns]
           #                 Name    Type 1  ... Speed  Generation  Legendary
    460  413  WormadamTrash Cloak       Bug  ...    36           4      False
    461  414               Mothim       Bug  ...    66           4      False
    462  415               Combee       Bug  ...    70           4      False
    463  416            Vespiquen       Bug  ...    40           4      False
    464  417            Pachirisu  Electric  ...    95           4      False
    465  418               Buizel     Water  ...    85           4      False
    466  419             Floatzel     Water  ...   115           4      False
    467  420              Cherubi     Grass  ...    35           4      False
    468  421              Cherrim     Grass  ...    85           4      False
    469  422              Shellos     Water  ...    34           4      False
    
    [10 rows x 13 columns]
           #                 Name  Type 1  ... Speed  Generation  Legendary
    470  423            Gastrodon   Water  ...    39           4      False
    471  424              Ambipom  Normal  ...   115           4      False
    472  425             Drifloon   Ghost  ...    70           4      False
    473  426             Drifblim   Ghost  ...    80           4      False
    474  427              Buneary  Normal  ...    85           4      False
    475  428              Lopunny  Normal  ...   105           4      False
    476  428  LopunnyMega Lopunny  Normal  ...   135           4      False
    477  429            Mismagius   Ghost  ...   105           4      False
    478  430            Honchkrow    Dark  ...    71           4      False
    479  431              Glameow  Normal  ...    85           4      False
    
    [10 rows x 13 columns]
           #       Name   Type 1   Type 2  ...  Sp. Def  Speed  Generation  Legendary
    480  432    Purugly   Normal      NaN  ...       59    112           4      False
    481  433  Chingling  Psychic      NaN  ...       50     45           4      False
    482  434     Stunky   Poison     Dark  ...       41     74           4      False
    483  435   Skuntank   Poison     Dark  ...       61     84           4      False
    484  436    Bronzor    Steel  Psychic  ...       86     23           4      False
    485  437   Bronzong    Steel  Psychic  ...      116     33           4      False
    486  438     Bonsly     Rock      NaN  ...       45     10           4      False
    487  439   Mime Jr.  Psychic    Fairy  ...       90     60           4      False
    488  440    Happiny   Normal      NaN  ...       65     30           4      False
    489  441     Chatot   Normal   Flying  ...       42     91           4      False
    
    [10 rows x 13 columns]
           #                   Name    Type 1  ... Speed  Generation  Legendary
    490  442              Spiritomb     Ghost  ...    35           4      False
    491  443                  Gible    Dragon  ...    42           4      False
    492  444                 Gabite    Dragon  ...    82           4      False
    493  445               Garchomp    Dragon  ...   102           4      False
    494  445  GarchompMega Garchomp    Dragon  ...    92           4      False
    495  446               Munchlax    Normal  ...     5           4      False
    496  447                  Riolu  Fighting  ...    60           4      False
    497  448                Lucario  Fighting  ...    90           4      False
    498  448    LucarioMega Lucario  Fighting  ...   112           4      False
    499  449             Hippopotas    Ground  ...    32           4      False
    
    [10 rows x 13 columns]
           #       Name  Type 1    Type 2  ...  Sp. Def  Speed  Generation  Legendary
    500  450  Hippowdon  Ground       NaN  ...       72     47           4      False
    501  451    Skorupi  Poison       Bug  ...       55     65           4      False
    502  452    Drapion  Poison      Dark  ...       75     95           4      False
    503  453   Croagunk  Poison  Fighting  ...       40     50           4      False
    504  454  Toxicroak  Poison  Fighting  ...       65     85           4      False
    505  455  Carnivine   Grass       NaN  ...       72     46           4      False
    506  456    Finneon   Water       NaN  ...       61     66           4      False
    507  457   Lumineon   Water       NaN  ...       86     91           4      False
    508  458    Mantyke   Water    Flying  ...      120     50           4      False
    509  459     Snover   Grass       Ice  ...       60     40           4      False
    
    [10 rows x 13 columns]
           #                     Name    Type 1  ... Speed  Generation  Legendary
    510  460                Abomasnow     Grass  ...    60           4      False
    511  460  AbomasnowMega Abomasnow     Grass  ...    30           4      False
    512  461                  Weavile      Dark  ...   125           4      False
    513  462                Magnezone  Electric  ...    60           4      False
    514  463               Lickilicky    Normal  ...    50           4      False
    515  464                Rhyperior    Ground  ...    40           4      False
    516  465                Tangrowth     Grass  ...    50           4      False
    517  466               Electivire  Electric  ...    95           4      False
    518  467                Magmortar      Fire  ...    83           4      False
    519  468                 Togekiss     Fairy  ...    80           4      False
    
    [10 rows x 13 columns]
           #                 Name   Type 1  ... Speed  Generation  Legendary
    520  469              Yanmega      Bug  ...    95           4      False
    521  470              Leafeon    Grass  ...    95           4      False
    522  471              Glaceon      Ice  ...    65           4      False
    523  472              Gliscor   Ground  ...    95           4      False
    524  473            Mamoswine      Ice  ...    80           4      False
    525  474            Porygon-Z   Normal  ...    90           4      False
    526  475              Gallade  Psychic  ...    80           4      False
    527  475  GalladeMega Gallade  Psychic  ...   110           4      False
    528  476            Probopass     Rock  ...    40           4      False
    529  477             Dusknoir    Ghost  ...    45           4      False
    
    [10 rows x 13 columns]
           #              Name    Type 1  ... Speed  Generation  Legendary
    530  478          Froslass       Ice  ...   110           4      False
    531  479             Rotom  Electric  ...    91           4      False
    532  479   RotomHeat Rotom  Electric  ...    86           4      False
    533  479   RotomWash Rotom  Electric  ...    86           4      False
    534  479  RotomFrost Rotom  Electric  ...    86           4      False
    535  479    RotomFan Rotom  Electric  ...    86           4      False
    536  479    RotomMow Rotom  Electric  ...    86           4      False
    537  480              Uxie   Psychic  ...    95           4       True
    538  481           Mesprit   Psychic  ...    80           4       True
    539  482             Azelf   Psychic  ...   115           4       True
    
    [10 rows x 13 columns]
           #                   Name   Type 1  ... Speed  Generation  Legendary
    540  483                 Dialga    Steel  ...    90           4       True
    541  484                 Palkia    Water  ...   100           4       True
    542  485                Heatran     Fire  ...    77           4       True
    543  486              Regigigas   Normal  ...   100           4       True
    544  487  GiratinaAltered Forme    Ghost  ...    90           4       True
    545  487   GiratinaOrigin Forme    Ghost  ...    90           4       True
    546  488              Cresselia  Psychic  ...    85           4      False
    547  489                 Phione    Water  ...    80           4      False
    548  490                Manaphy    Water  ...   100           4      False
    549  491                Darkrai     Dark  ...   125           4       True
    
    [10 rows x 13 columns]
           #               Name   Type 1  ... Speed  Generation  Legendary
    550  492  ShayminLand Forme    Grass  ...   100           4       True
    551  492   ShayminSky Forme    Grass  ...   127           4       True
    552  493             Arceus   Normal  ...   120           4       True
    553  494            Victini  Psychic  ...   100           5       True
    554  495              Snivy    Grass  ...    63           5      False
    555  496            Servine    Grass  ...    83           5      False
    556  497          Serperior    Grass  ...   113           5      False
    557  498              Tepig     Fire  ...    45           5      False
    558  499            Pignite     Fire  ...    55           5      False
    559  500             Emboar     Fire  ...    65           5      False
    
    [10 rows x 13 columns]
           #       Name  Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    560  501   Oshawott   Water     NaN  ...       45     45           5      False
    561  502     Dewott   Water     NaN  ...       60     60           5      False
    562  503   Samurott   Water     NaN  ...       70     70           5      False
    563  504     Patrat  Normal     NaN  ...       39     42           5      False
    564  505    Watchog  Normal     NaN  ...       69     77           5      False
    565  506   Lillipup  Normal     NaN  ...       45     55           5      False
    566  507    Herdier  Normal     NaN  ...       65     60           5      False
    567  508  Stoutland  Normal     NaN  ...       90     80           5      False
    568  509   Purrloin    Dark     NaN  ...       37     66           5      False
    569  510    Liepard    Dark     NaN  ...       50    106           5      False
    
    [10 rows x 13 columns]
           #       Name   Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    570  511    Pansage    Grass     NaN  ...       48     64           5      False
    571  512   Simisage    Grass     NaN  ...       63    101           5      False
    572  513    Pansear     Fire     NaN  ...       48     64           5      False
    573  514   Simisear     Fire     NaN  ...       63    101           5      False
    574  515    Panpour    Water     NaN  ...       48     64           5      False
    575  516   Simipour    Water     NaN  ...       63    101           5      False
    576  517      Munna  Psychic     NaN  ...       55     24           5      False
    577  518   Musharna  Psychic     NaN  ...       95     29           5      False
    578  519     Pidove   Normal  Flying  ...       30     43           5      False
    579  520  Tranquill   Normal  Flying  ...       42     65           5      False
    
    [10 rows x 13 columns]
           #        Name    Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    580  521    Unfezant    Normal  Flying  ...       55     93           5      False
    581  522     Blitzle  Electric     NaN  ...       32     76           5      False
    582  523   Zebstrika  Electric     NaN  ...       63    116           5      False
    583  524  Roggenrola      Rock     NaN  ...       25     15           5      False
    584  525     Boldore      Rock     NaN  ...       40     20           5      False
    585  526    Gigalith      Rock     NaN  ...       80     25           5      False
    586  527      Woobat   Psychic  Flying  ...       43     72           5      False
    587  528     Swoobat   Psychic  Flying  ...       55    114           5      False
    588  529     Drilbur    Ground     NaN  ...       45     68           5      False
    589  530   Excadrill    Ground   Steel  ...       65     88           5      False
    
    [10 rows x 13 columns]
           #               Name    Type 1  ... Speed  Generation  Legendary
    590  531             Audino    Normal  ...    50           5      False
    591  531  AudinoMega Audino    Normal  ...    50           5      False
    592  532            Timburr  Fighting  ...    35           5      False
    593  533            Gurdurr  Fighting  ...    40           5      False
    594  534         Conkeldurr  Fighting  ...    45           5      False
    595  535            Tympole     Water  ...    64           5      False
    596  536          Palpitoad     Water  ...    69           5      False
    597  537         Seismitoad     Water  ...    74           5      False
    598  538              Throh  Fighting  ...    45           5      False
    599  539               Sawk  Fighting  ...    85           5      False
    
    [10 rows x 13 columns]
           #        Name Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    600  540    Sewaddle    Bug   Grass  ...       60     42           5      False
    601  541    Swadloon    Bug   Grass  ...       80     42           5      False
    602  542    Leavanny    Bug   Grass  ...       80     92           5      False
    603  543    Venipede    Bug  Poison  ...       39     57           5      False
    604  544  Whirlipede    Bug  Poison  ...       79     47           5      False
    605  545   Scolipede    Bug  Poison  ...       69    112           5      False
    606  546    Cottonee  Grass   Fairy  ...       50     66           5      False
    607  547  Whimsicott  Grass   Fairy  ...       75    116           5      False
    608  548     Petilil  Grass     NaN  ...       50     30           5      False
    609  549   Lilligant  Grass     NaN  ...       75     90           5      False
    
    [10 rows x 13 columns]
           #                     Name  Type 1  ... Speed  Generation  Legendary
    610  550                 Basculin   Water  ...    98           5      False
    611  551                  Sandile  Ground  ...    65           5      False
    612  552                 Krokorok  Ground  ...    74           5      False
    613  553               Krookodile  Ground  ...    92           5      False
    614  554                 Darumaka    Fire  ...    50           5      False
    615  555  DarmanitanStandard Mode    Fire  ...    95           5      False
    616  555       DarmanitanZen Mode    Fire  ...    55           5      False
    617  556                 Maractus   Grass  ...    60           5      False
    618  557                  Dwebble     Bug  ...    55           5      False
    619  558                  Crustle     Bug  ...    45           5      False
    
    [10 rows x 13 columns]
           #        Name   Type 1    Type 2  ...  Sp. Def  Speed  Generation  Legendary
    620  559     Scraggy     Dark  Fighting  ...       70     48           5      False
    621  560     Scrafty     Dark  Fighting  ...      115     58           5      False
    622  561    Sigilyph  Psychic    Flying  ...       80     97           5      False
    623  562      Yamask    Ghost       NaN  ...       65     30           5      False
    624  563  Cofagrigus    Ghost       NaN  ...      105     30           5      False
    625  564    Tirtouga    Water      Rock  ...       45     22           5      False
    626  565  Carracosta    Water      Rock  ...       65     32           5      False
    627  566      Archen     Rock    Flying  ...       45     70           5      False
    628  567    Archeops     Rock    Flying  ...       65    110           5      False
    629  568    Trubbish   Poison       NaN  ...       62     65           5      False
    
    [10 rows x 13 columns]
           #        Name   Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    630  569    Garbodor   Poison     NaN  ...       82     75           5      False
    631  570       Zorua     Dark     NaN  ...       40     65           5      False
    632  571     Zoroark     Dark     NaN  ...       60    105           5      False
    633  572    Minccino   Normal     NaN  ...       40     75           5      False
    634  573    Cinccino   Normal     NaN  ...       60    115           5      False
    635  574     Gothita  Psychic     NaN  ...       65     45           5      False
    636  575   Gothorita  Psychic     NaN  ...       85     55           5      False
    637  576  Gothitelle  Psychic     NaN  ...      110     65           5      False
    638  577     Solosis  Psychic     NaN  ...       50     20           5      False
    639  578     Duosion  Psychic     NaN  ...       60     30           5      False
    
    [10 rows x 13 columns]
           #        Name    Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    640  579   Reuniclus   Psychic     NaN  ...       85     30           5      False
    641  580    Ducklett     Water  Flying  ...       50     55           5      False
    642  581      Swanna     Water  Flying  ...       63     98           5      False
    643  582   Vanillite       Ice     NaN  ...       60     44           5      False
    644  583   Vanillish       Ice     NaN  ...       75     59           5      False
    645  584   Vanilluxe       Ice     NaN  ...       95     79           5      False
    646  585    Deerling    Normal   Grass  ...       50     75           5      False
    647  586    Sawsbuck    Normal   Grass  ...       70     95           5      False
    648  587      Emolga  Electric  Flying  ...       60    103           5      False
    649  588  Karrablast       Bug     NaN  ...       45     60           5      False
    
    [10 rows x 13 columns]
           #        Name Type 1    Type 2  ...  Sp. Def  Speed  Generation  Legendary
    650  589  Escavalier    Bug     Steel  ...      105     20           5      False
    651  590     Foongus  Grass    Poison  ...       55     15           5      False
    652  591   Amoonguss  Grass    Poison  ...       80     30           5      False
    653  592    Frillish  Water     Ghost  ...       85     40           5      False
    654  593   Jellicent  Water     Ghost  ...      105     60           5      False
    655  594   Alomomola  Water       NaN  ...       45     65           5      False
    656  595      Joltik    Bug  Electric  ...       50     65           5      False
    657  596  Galvantula    Bug  Electric  ...       60    108           5      False
    658  597   Ferroseed  Grass     Steel  ...       86     10           5      False
    659  598  Ferrothorn  Grass     Steel  ...      116     20           5      False
    
    [10 rows x 13 columns]
           #        Name    Type 1 Type 2  ...  Sp. Def  Speed  Generation  Legendary
    660  599       Klink     Steel    NaN  ...       60     30           5      False
    661  600       Klang     Steel    NaN  ...       85     50           5      False
    662  601   Klinklang     Steel    NaN  ...       85     90           5      False
    663  602      Tynamo  Electric    NaN  ...       40     60           5      False
    664  603   Eelektrik  Electric    NaN  ...       70     40           5      False
    665  604  Eelektross  Electric    NaN  ...       80     50           5      False
    666  605      Elgyem   Psychic    NaN  ...       55     30           5      False
    667  606    Beheeyem   Psychic    NaN  ...       95     40           5      False
    668  607     Litwick     Ghost   Fire  ...       55     20           5      False
    669  608     Lampent     Ghost   Fire  ...       60     55           5      False
    
    [10 rows x 13 columns]
           #        Name  Type 1    Type 2  ...  Sp. Def  Speed  Generation  Legendary
    670  609  Chandelure   Ghost      Fire  ...       90     80           5      False
    671  610        Axew  Dragon       NaN  ...       40     57           5      False
    672  611     Fraxure  Dragon       NaN  ...       50     67           5      False
    673  612     Haxorus  Dragon       NaN  ...       70     97           5      False
    674  613     Cubchoo     Ice       NaN  ...       40     40           5      False
    675  614     Beartic     Ice       NaN  ...       80     50           5      False
    676  615   Cryogonal     Ice       NaN  ...      135    105           5      False
    677  616     Shelmet     Bug       NaN  ...       65     25           5      False
    678  617    Accelgor     Bug       NaN  ...       60    145           5      False
    679  618    Stunfisk  Ground  Electric  ...       99     32           5      False
    
    [10 rows x 13 columns]
           #        Name    Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    680  619     Mienfoo  Fighting     NaN  ...       50     65           5      False
    681  620    Mienshao  Fighting     NaN  ...       60    105           5      False
    682  621   Druddigon    Dragon     NaN  ...       90     48           5      False
    683  622      Golett    Ground   Ghost  ...       50     35           5      False
    684  623      Golurk    Ground   Ghost  ...       80     55           5      False
    685  624    Pawniard      Dark   Steel  ...       40     60           5      False
    686  625     Bisharp      Dark   Steel  ...       70     70           5      False
    687  626  Bouffalant    Normal     NaN  ...       95     55           5      False
    688  627     Rufflet    Normal  Flying  ...       50     60           5      False
    689  628    Braviary    Normal  Flying  ...       75     80           5      False
    
    [10 rows x 13 columns]
           #       Name Type 1    Type 2  ...  Sp. Def  Speed  Generation  Legendary
    690  629    Vullaby   Dark    Flying  ...       65     60           5      False
    691  630  Mandibuzz   Dark    Flying  ...       95     80           5      False
    692  631    Heatmor   Fire       NaN  ...       66     65           5      False
    693  632     Durant    Bug     Steel  ...       48    109           5      False
    694  633      Deino   Dark    Dragon  ...       50     38           5      False
    695  634   Zweilous   Dark    Dragon  ...       70     58           5      False
    696  635  Hydreigon   Dark    Dragon  ...       90     98           5      False
    697  636   Larvesta    Bug      Fire  ...       55     60           5      False
    698  637  Volcarona    Bug      Fire  ...      105    100           5      False
    699  638   Cobalion  Steel  Fighting  ...       72    108           5       True
    
    [10 rows x 13 columns]
           #                      Name    Type 1  ... Speed  Generation  Legendary
    700  639                 Terrakion      Rock  ...   108           5       True
    701  640                  Virizion     Grass  ...   108           5       True
    702  641   TornadusIncarnate Forme    Flying  ...   111           5       True
    703  641     TornadusTherian Forme    Flying  ...   121           5       True
    704  642  ThundurusIncarnate Forme  Electric  ...   111           5       True
    705  642    ThundurusTherian Forme  Electric  ...   101           5       True
    706  643                  Reshiram    Dragon  ...    90           5       True
    707  644                    Zekrom    Dragon  ...    90           5       True
    708  645   LandorusIncarnate Forme    Ground  ...   101           5       True
    709  645     LandorusTherian Forme    Ground  ...    91           5       True
    
    [10 rows x 13 columns]
           #                     Name  Type 1  ... Speed  Generation  Legendary
    710  646                   Kyurem  Dragon  ...    95           5       True
    711  646       KyuremBlack Kyurem  Dragon  ...    95           5       True
    712  646       KyuremWhite Kyurem  Dragon  ...    95           5       True
    713  647     KeldeoOrdinary Forme   Water  ...   108           5      False
    714  647     KeldeoResolute Forme   Water  ...   108           5      False
    715  648       MeloettaAria Forme  Normal  ...    90           5      False
    716  648  MeloettaPirouette Forme  Normal  ...   128           5      False
    717  649                 Genesect     Bug  ...    99           5      False
    718  650                  Chespin   Grass  ...    38           6      False
    719  651                Quilladin   Grass  ...    57           6      False
    
    [10 rows x 13 columns]
           #        Name  Type 1    Type 2  ...  Sp. Def  Speed  Generation  Legendary
    720  652  Chesnaught   Grass  Fighting  ...       75     64           6      False
    721  653    Fennekin    Fire       NaN  ...       60     60           6      False
    722  654     Braixen    Fire       NaN  ...       70     73           6      False
    723  655     Delphox    Fire   Psychic  ...      100    104           6      False
    724  656     Froakie   Water       NaN  ...       44     71           6      False
    725  657   Frogadier   Water       NaN  ...       56     97           6      False
    726  658    Greninja   Water      Dark  ...       71    122           6      False
    727  659    Bunnelby  Normal       NaN  ...       36     57           6      False
    728  660   Diggersby  Normal    Ground  ...       77     78           6      False
    729  661  Fletchling  Normal    Flying  ...       38     62           6      False
    
    [10 rows x 13 columns]
           #         Name Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    730  662  Fletchinder   Fire  Flying  ...       52     84           6      False
    731  663   Talonflame   Fire  Flying  ...       69    126           6      False
    732  664   Scatterbug    Bug     NaN  ...       25     35           6      False
    733  665       Spewpa    Bug     NaN  ...       30     29           6      False
    734  666     Vivillon    Bug  Flying  ...       50     89           6      False
    735  667       Litleo   Fire  Normal  ...       54     72           6      False
    736  668       Pyroar   Fire  Normal  ...       66    106           6      False
    737  669      Flabébé  Fairy     NaN  ...       79     42           6      False
    738  670      Floette  Fairy     NaN  ...       98     52           6      False
    739  671      Florges  Fairy     NaN  ...      154     75           6      False
    
    [10 rows x 13 columns]
           #            Name    Type 1  ... Speed  Generation  Legendary
    740  672          Skiddo     Grass  ...    52           6      False
    741  673          Gogoat     Grass  ...    68           6      False
    742  674         Pancham  Fighting  ...    43           6      False
    743  675         Pangoro  Fighting  ...    58           6      False
    744  676         Furfrou    Normal  ...   102           6      False
    745  677          Espurr   Psychic  ...    68           6      False
    746  678    MeowsticMale   Psychic  ...   104           6      False
    747  678  MeowsticFemale   Psychic  ...   104           6      False
    748  679         Honedge     Steel  ...    28           6      False
    749  680        Doublade     Steel  ...    35           6      False
    
    [10 rows x 13 columns]
           #                   Name Type 1  ... Speed  Generation  Legendary
    750  681   AegislashBlade Forme  Steel  ...    60           6      False
    751  681  AegislashShield Forme  Steel  ...    60           6      False
    752  682               Spritzee  Fairy  ...    23           6      False
    753  683             Aromatisse  Fairy  ...    29           6      False
    754  684                Swirlix  Fairy  ...    49           6      False
    755  685               Slurpuff  Fairy  ...    72           6      False
    756  686                  Inkay   Dark  ...    45           6      False
    757  687                Malamar   Dark  ...    73           6      False
    758  688                Binacle   Rock  ...    50           6      False
    759  689             Barbaracle   Rock  ...    68           6      False
    
    [10 rows x 13 columns]
           #        Name    Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    760  690      Skrelp    Poison   Water  ...       60     30           6      False
    761  691    Dragalge    Poison  Dragon  ...      123     44           6      False
    762  692   Clauncher     Water     NaN  ...       63     44           6      False
    763  693   Clawitzer     Water     NaN  ...       89     59           6      False
    764  694  Helioptile  Electric  Normal  ...       43     70           6      False
    765  695   Heliolisk  Electric  Normal  ...       94    109           6      False
    766  696      Tyrunt      Rock  Dragon  ...       45     48           6      False
    767  697   Tyrantrum      Rock  Dragon  ...       59     71           6      False
    768  698      Amaura      Rock     Ice  ...       63     46           6      False
    769  699     Aurorus      Rock     Ice  ...       92     58           6      False
    
    [10 rows x 13 columns]
           #       Name    Type 1  Type 2  ...  Sp. Def  Speed  Generation  Legendary
    770  700    Sylveon     Fairy     NaN  ...      130     60           6      False
    771  701   Hawlucha  Fighting  Flying  ...       63    118           6      False
    772  702    Dedenne  Electric   Fairy  ...       67    101           6      False
    773  703    Carbink      Rock   Fairy  ...      150     50           6      False
    774  704      Goomy    Dragon     NaN  ...       75     40           6      False
    775  705    Sliggoo    Dragon     NaN  ...      113     60           6      False
    776  706     Goodra    Dragon     NaN  ...      150     80           6      False
    777  707     Klefki     Steel   Fairy  ...       87     75           6      False
    778  708   Phantump     Ghost   Grass  ...       60     38           6      False
    779  709  Trevenant     Ghost   Grass  ...       82     56           6      False
    
    [10 rows x 13 columns]
           #                   Name Type 1  ... Speed  Generation  Legendary
    780  710  PumpkabooAverage Size  Ghost  ...    51           6      False
    781  710    PumpkabooSmall Size  Ghost  ...    56           6      False
    782  710    PumpkabooLarge Size  Ghost  ...    46           6      False
    783  710    PumpkabooSuper Size  Ghost  ...    41           6      False
    784  711  GourgeistAverage Size  Ghost  ...    84           6      False
    785  711    GourgeistSmall Size  Ghost  ...    99           6      False
    786  711    GourgeistLarge Size  Ghost  ...    69           6      False
    787  711    GourgeistSuper Size  Ghost  ...    54           6      False
    788  712               Bergmite    Ice  ...    28           6      False
    789  713                Avalugg    Ice  ...    28           6      False
    
    [10 rows x 13 columns]
           #                 Name   Type 1  ... Speed  Generation  Legendary
    790  714               Noibat   Flying  ...    55           6      False
    791  715              Noivern   Flying  ...   123           6      False
    792  716              Xerneas    Fairy  ...    99           6       True
    793  717              Yveltal     Dark  ...    99           6       True
    794  718     Zygarde50% Forme   Dragon  ...    95           6       True
    795  719              Diancie     Rock  ...    50           6       True
    796  719  DiancieMega Diancie     Rock  ...   110           6       True
    797  720  HoopaHoopa Confined  Psychic  ...    70           6       True
    798  720   HoopaHoopa Unbound  Psychic  ...    80           6       True
    799  721            Volcanion     Fire  ...    70           6       True
    
    [10 rows x 13 columns]
    


```python
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>790</th>
      <td>714</td>
      <td>Noibat</td>
      <td>Flying</td>
      <td>Dragon</td>
      <td>260</td>
      <td>40</td>
      <td>30</td>
      <td>35</td>
      <td>45</td>
      <td>40</td>
      <td>55</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>791</th>
      <td>715</td>
      <td>Noivern</td>
      <td>Flying</td>
      <td>Dragon</td>
      <td>567</td>
      <td>85</td>
      <td>70</td>
      <td>80</td>
      <td>97</td>
      <td>80</td>
      <td>123</td>
      <td>6</td>
      <td>False</td>
    </tr>
    <tr>
      <th>792</th>
      <td>716</td>
      <td>Xerneas</td>
      <td>Fairy</td>
      <td>NaN</td>
      <td>838</td>
      <td>126</td>
      <td>131</td>
      <td>95</td>
      <td>131</td>
      <td>98</td>
      <td>99</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>793</th>
      <td>717</td>
      <td>Yveltal</td>
      <td>Dark</td>
      <td>Flying</td>
      <td>838</td>
      <td>126</td>
      <td>131</td>
      <td>95</td>
      <td>131</td>
      <td>98</td>
      <td>99</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>794</th>
      <td>718</td>
      <td>Zygarde50% Forme</td>
      <td>Dragon</td>
      <td>Ground</td>
      <td>713</td>
      <td>108</td>
      <td>100</td>
      <td>121</td>
      <td>81</td>
      <td>95</td>
      <td>95</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>795</th>
      <td>719</td>
      <td>Diancie</td>
      <td>Rock</td>
      <td>Fairy</td>
      <td>700</td>
      <td>50</td>
      <td>100</td>
      <td>150</td>
      <td>100</td>
      <td>150</td>
      <td>50</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>796</th>
      <td>719</td>
      <td>DiancieMega Diancie</td>
      <td>Rock</td>
      <td>Fairy</td>
      <td>800</td>
      <td>50</td>
      <td>160</td>
      <td>110</td>
      <td>160</td>
      <td>110</td>
      <td>110</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>797</th>
      <td>720</td>
      <td>HoopaHoopa Confined</td>
      <td>Psychic</td>
      <td>Ghost</td>
      <td>720</td>
      <td>80</td>
      <td>110</td>
      <td>60</td>
      <td>150</td>
      <td>130</td>
      <td>70</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>798</th>
      <td>720</td>
      <td>HoopaHoopa Unbound</td>
      <td>Psychic</td>
      <td>Dark</td>
      <td>840</td>
      <td>80</td>
      <td>160</td>
      <td>60</td>
      <td>170</td>
      <td>130</td>
      <td>80</td>
      <td>6</td>
      <td>True</td>
    </tr>
    <tr>
      <th>799</th>
      <td>721</td>
      <td>Volcanion</td>
      <td>Fire</td>
      <td>Water</td>
      <td>720</td>
      <td>80</td>
      <td>110</td>
      <td>120</td>
      <td>130</td>
      <td>90</td>
      <td>70</td>
      <td>6</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1 = pd.DataFrame()
for df in pd.read_csv('poke_updated1.csv', chunksize=10):
    df1 = pd.concat([df1 ,df])
df1.head(15)
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Generation</th>
      <th>Legendary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>367</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>467</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>607</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>725</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>335</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>447</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Charizard</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>596</td>
      <td>78</td>
      <td>84</td>
      <td>78</td>
      <td>109</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>CharizardMega Charizard X</td>
      <td>Fire</td>
      <td>Dragon</td>
      <td>742</td>
      <td>78</td>
      <td>130</td>
      <td>111</td>
      <td>130</td>
      <td>85</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>8</th>
      <td>6</td>
      <td>CharizardMega Charizard Y</td>
      <td>Fire</td>
      <td>Flying</td>
      <td>716</td>
      <td>78</td>
      <td>104</td>
      <td>78</td>
      <td>159</td>
      <td>115</td>
      <td>100</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7</td>
      <td>Squirtle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>363</td>
      <td>44</td>
      <td>48</td>
      <td>65</td>
      <td>50</td>
      <td>64</td>
      <td>43</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>8</td>
      <td>Wartortle</td>
      <td>Water</td>
      <td>NaN</td>
      <td>469</td>
      <td>59</td>
      <td>63</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
      <td>58</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>11</th>
      <td>9</td>
      <td>Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>614</td>
      <td>79</td>
      <td>83</td>
      <td>100</td>
      <td>85</td>
      <td>105</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>12</th>
      <td>9</td>
      <td>BlastoiseMega Blastoise</td>
      <td>Water</td>
      <td>NaN</td>
      <td>734</td>
      <td>79</td>
      <td>103</td>
      <td>120</td>
      <td>135</td>
      <td>115</td>
      <td>78</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>13</th>
      <td>10</td>
      <td>Caterpie</td>
      <td>Bug</td>
      <td>NaN</td>
      <td>225</td>
      <td>45</td>
      <td>30</td>
      <td>35</td>
      <td>20</td>
      <td>20</td>
      <td>45</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>14</th>
      <td>11</td>
      <td>Metapod</td>
      <td>Bug</td>
      <td>NaN</td>
      <td>245</td>
      <td>50</td>
      <td>20</td>
      <td>55</td>
      <td>25</td>
      <td>25</td>
      <td>30</td>
      <td>1</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



# Stack & unstack in Pandas


```python
col = pd.MultiIndex.from_product([['2010','2015'],['Literacy' , 'GDP']])

data =([[80,7,88,6],[90,8,92,7],[89,7,91,8],[87,6,93,8]])

df6 = pd.DataFrame(data, index=['India','USA' , 'Russia' , 'China'], columns=col)
df6
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">2010</th>
      <th colspan="2" halign="left">2015</th>
    </tr>
    <tr>
      <th></th>
      <th>Literacy</th>
      <th>GDP</th>
      <th>Literacy</th>
      <th>GDP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>India</th>
      <td>80</td>
      <td>7</td>
      <td>88</td>
      <td>6</td>
    </tr>
    <tr>
      <th>USA</th>
      <td>90</td>
      <td>8</td>
      <td>92</td>
      <td>7</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>89</td>
      <td>7</td>
      <td>91</td>
      <td>8</td>
    </tr>
    <tr>
      <th>China</th>
      <td>87</td>
      <td>6</td>
      <td>93</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Stack() Function stacks the columns to rows.
st_df = df6.stack()
st_df
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
      <th>2010</th>
      <th>2015</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">India</th>
      <th>GDP</th>
      <td>7</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>80</td>
      <td>88</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">USA</th>
      <th>GDP</th>
      <td>8</td>
      <td>7</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>90</td>
      <td>92</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Russia</th>
      <th>GDP</th>
      <td>7</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>89</td>
      <td>91</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">China</th>
      <th>GDP</th>
      <td>6</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>87</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Unstacks the row to columns
unst_df = st_df.unstack()
unst_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">2010</th>
      <th colspan="2" halign="left">2015</th>
    </tr>
    <tr>
      <th></th>
      <th>GDP</th>
      <th>Literacy</th>
      <th>GDP</th>
      <th>Literacy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>China</th>
      <td>6</td>
      <td>87</td>
      <td>8</td>
      <td>93</td>
    </tr>
    <tr>
      <th>India</th>
      <td>7</td>
      <td>80</td>
      <td>6</td>
      <td>88</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>7</td>
      <td>89</td>
      <td>8</td>
      <td>91</td>
    </tr>
    <tr>
      <th>USA</th>
      <td>8</td>
      <td>90</td>
      <td>7</td>
      <td>92</td>
    </tr>
  </tbody>
</table>
</div>




```python
unst_df = unst_df.unstack()
unst_df
```




    2010  GDP       China      6
                    India      7
                    Russia     7
                    USA        8
          Literacy  China     87
                    India     80
                    Russia    89
                    USA       90
    2015  GDP       China      8
                    India      6
                    Russia     8
                    USA        7
          Literacy  China     93
                    India     88
                    Russia    91
                    USA       92
    dtype: int64




```python
unst_df = unst_df.unstack()
unst_df
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
      <th>China</th>
      <th>India</th>
      <th>Russia</th>
      <th>USA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">2010</th>
      <th>GDP</th>
      <td>6</td>
      <td>7</td>
      <td>7</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>87</td>
      <td>80</td>
      <td>89</td>
      <td>90</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2015</th>
      <th>GDP</th>
      <td>8</td>
      <td>6</td>
      <td>8</td>
      <td>7</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>93</td>
      <td>88</td>
      <td>91</td>
      <td>92</td>
    </tr>
  </tbody>
</table>
</div>



# PIVOT Tables


```python
data = {
    'Country':['India','USA' , 'Russia' , 'China','India','USA' , 'Russia' , 'China','India','USA' , 'Russia' , 'China','India','USA' , 'Russia' , 'China'],
    'Year':['2010','2010','2010','2010' , '2010','2010','2010','2010','2015','2015','2015','2015','2015','2015','2015','2015'],
     
    'Literacy/GDP':['GDP' , 'GDP' , 'GDP' , 'GDP','Literacy' , 'Literacy', 'Literacy' , 'Literacy','GDP' , 'GDP','GDP' , 'GDP','Literacy' , 'Literacy','Literacy' , 'Literacy'],
   'Value':[7,8,7,6,80,90,89,87,6,7,8, 8, 88 , 92 , 91 ,93]}
 
df7 = pd.DataFrame(data,columns=['Country','Year','Literacy/GDP','Value'])
df7
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
      <th>Country</th>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>India</td>
      <td>2010</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>USA</td>
      <td>2010</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Russia</td>
      <td>2010</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>China</td>
      <td>2010</td>
      <td>GDP</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>India</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>USA</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>90</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Russia</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>89</td>
    </tr>
    <tr>
      <th>7</th>
      <td>China</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>87</td>
    </tr>
    <tr>
      <th>8</th>
      <td>India</td>
      <td>2015</td>
      <td>GDP</td>
      <td>6</td>
    </tr>
    <tr>
      <th>9</th>
      <td>USA</td>
      <td>2015</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Russia</td>
      <td>2015</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>11</th>
      <td>China</td>
      <td>2015</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>12</th>
      <td>India</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>88</td>
    </tr>
    <tr>
      <th>13</th>
      <td>USA</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>92</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Russia</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>91</td>
    </tr>
    <tr>
      <th>15</th>
      <td>China</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Pivot table with SUM aggregation
pd.pivot_table(df7 , index= ['Year' , 'Literacy/GDP'] , aggfunc='sum')
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
      <th>Value</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">2010</th>
      <th>GDP</th>
      <td>28</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>346</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2015</th>
      <th>GDP</th>
      <td>29</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>364</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Pivot table with MEAN aggregation
pd.pivot_table(df7 , index= ['Year' , 'Literacy/GDP'] , aggfunc='mean')
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
      <th>Value</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">2010</th>
      <th>GDP</th>
      <td>7.00</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>86.50</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2015</th>
      <th>GDP</th>
      <td>7.25</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>91.00</td>
    </tr>
  </tbody>
</table>
</div>



# Hierarchical indexing


```python
df7
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
      <th>Country</th>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>India</td>
      <td>2010</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>USA</td>
      <td>2010</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Russia</td>
      <td>2010</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>China</td>
      <td>2010</td>
      <td>GDP</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>India</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>USA</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>90</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Russia</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>89</td>
    </tr>
    <tr>
      <th>7</th>
      <td>China</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>87</td>
    </tr>
    <tr>
      <th>8</th>
      <td>India</td>
      <td>2015</td>
      <td>GDP</td>
      <td>6</td>
    </tr>
    <tr>
      <th>9</th>
      <td>USA</td>
      <td>2015</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Russia</td>
      <td>2015</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>11</th>
      <td>China</td>
      <td>2015</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>12</th>
      <td>India</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>88</td>
    </tr>
    <tr>
      <th>13</th>
      <td>USA</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>92</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Russia</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>91</td>
    </tr>
    <tr>
      <th>15</th>
      <td>China</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




```python
df8=df7.set_index(['Year', 'Literacy/GDP'])
df8
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
      <th>Country</th>
      <th>Value</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">2010</th>
      <th>GDP</th>
      <td>India</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>USA</td>
      <td>8</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>Russia</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>China</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>India</td>
      <td>80</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>USA</td>
      <td>90</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>Russia</td>
      <td>89</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>China</td>
      <td>87</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">2015</th>
      <th>GDP</th>
      <td>India</td>
      <td>6</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>USA</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>Russia</td>
      <td>8</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>China</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>India</td>
      <td>88</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>USA</td>
      <td>92</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>Russia</td>
      <td>91</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>China</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




```python
df8.index
```




    MultiIndex([('2010',      'GDP'),
                ('2010',      'GDP'),
                ('2010',      'GDP'),
                ('2010',      'GDP'),
                ('2010', 'Literacy'),
                ('2010', 'Literacy'),
                ('2010', 'Literacy'),
                ('2010', 'Literacy'),
                ('2015',      'GDP'),
                ('2015',      'GDP'),
                ('2015',      'GDP'),
                ('2015',      'GDP'),
                ('2015', 'Literacy'),
                ('2015', 'Literacy'),
                ('2015', 'Literacy'),
                ('2015', 'Literacy')],
               names=['Year', 'Literacy/GDP'])




```python
df8.loc['2010']
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
      <th>Country</th>
      <th>Value</th>
    </tr>
    <tr>
      <th>Literacy/GDP</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>GDP</th>
      <td>India</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>USA</td>
      <td>8</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>Russia</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>China</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>India</td>
      <td>80</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>USA</td>
      <td>90</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>Russia</td>
      <td>89</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>China</td>
      <td>87</td>
    </tr>
  </tbody>
</table>
</div>




```python
df8.loc[['2010']]
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
      <th>Country</th>
      <th>Value</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">2010</th>
      <th>GDP</th>
      <td>India</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>USA</td>
      <td>8</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>Russia</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>China</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>India</td>
      <td>80</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>USA</td>
      <td>90</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>Russia</td>
      <td>89</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>China</td>
      <td>87</td>
    </tr>
  </tbody>
</table>
</div>




```python
df8.loc['2015','Literacy']
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
      <th>Country</th>
      <th>Value</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">2015</th>
      <th>Literacy</th>
      <td>India</td>
      <td>88</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>USA</td>
      <td>92</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>Russia</td>
      <td>91</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>China</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




```python
df8.loc['2015','Literacy']
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
      <th>Country</th>
      <th>Value</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">2015</th>
      <th>Literacy</th>
      <td>India</td>
      <td>88</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>USA</td>
      <td>92</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>Russia</td>
      <td>91</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>China</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




```python
df8=df7.set_index(['Year', 'Literacy/GDP' , 'Country'])
df8
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
      <th></th>
      <th>Value</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th>Country</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">2010</th>
      <th rowspan="4" valign="top">GDP</th>
      <th>India</th>
      <td>7</td>
    </tr>
    <tr>
      <th>USA</th>
      <td>8</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>7</td>
    </tr>
    <tr>
      <th>China</th>
      <td>6</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Literacy</th>
      <th>India</th>
      <td>80</td>
    </tr>
    <tr>
      <th>USA</th>
      <td>90</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>89</td>
    </tr>
    <tr>
      <th>China</th>
      <td>87</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">2015</th>
      <th rowspan="4" valign="top">GDP</th>
      <th>India</th>
      <td>6</td>
    </tr>
    <tr>
      <th>USA</th>
      <td>7</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>8</td>
    </tr>
    <tr>
      <th>China</th>
      <td>8</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Literacy</th>
      <th>India</th>
      <td>88</td>
    </tr>
    <tr>
      <th>USA</th>
      <td>92</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>91</td>
    </tr>
    <tr>
      <th>China</th>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>



### SWAP Columns in Hierarchical indexing


```python
df7
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
      <th>Country</th>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>India</td>
      <td>2010</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>USA</td>
      <td>2010</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Russia</td>
      <td>2010</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>China</td>
      <td>2010</td>
      <td>GDP</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>India</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>USA</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>90</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Russia</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>89</td>
    </tr>
    <tr>
      <th>7</th>
      <td>China</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>87</td>
    </tr>
    <tr>
      <th>8</th>
      <td>India</td>
      <td>2015</td>
      <td>GDP</td>
      <td>6</td>
    </tr>
    <tr>
      <th>9</th>
      <td>USA</td>
      <td>2015</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Russia</td>
      <td>2015</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>11</th>
      <td>China</td>
      <td>2015</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>12</th>
      <td>India</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>88</td>
    </tr>
    <tr>
      <th>13</th>
      <td>USA</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>92</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Russia</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>91</td>
    </tr>
    <tr>
      <th>15</th>
      <td>China</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




```python
df8=df7.set_index(['Year', 'Literacy/GDP'])
df8
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
      <th>Country</th>
      <th>Value</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">2010</th>
      <th>GDP</th>
      <td>India</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>USA</td>
      <td>8</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>Russia</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>China</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>India</td>
      <td>80</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>USA</td>
      <td>90</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>Russia</td>
      <td>89</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>China</td>
      <td>87</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">2015</th>
      <th>GDP</th>
      <td>India</td>
      <td>6</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>USA</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>Russia</td>
      <td>8</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>China</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>India</td>
      <td>88</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>USA</td>
      <td>92</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>Russia</td>
      <td>91</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>China</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Swaping the columns in Hierarchical index
df9 = df8.swaplevel('Year', 'Literacy/GDP')
df9
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
      <th>Country</th>
      <th>Value</th>
    </tr>
    <tr>
      <th>Literacy/GDP</th>
      <th>Year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">GDP</th>
      <th>2010</th>
      <td>India</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>USA</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>Russia</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>China</td>
      <td>6</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Literacy</th>
      <th>2010</th>
      <td>India</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>USA</td>
      <td>90</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>Russia</td>
      <td>89</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>China</td>
      <td>87</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">GDP</th>
      <th>2015</th>
      <td>India</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>USA</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>Russia</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>China</td>
      <td>8</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Literacy</th>
      <th>2015</th>
      <td>India</td>
      <td>88</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>USA</td>
      <td>92</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>Russia</td>
      <td>91</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>China</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Swaping the columns in Hierarchical index
df9 = df9.swaplevel('Year', 'Literacy/GDP')
df9
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
      <th>Country</th>
      <th>Value</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="8" valign="top">2010</th>
      <th>GDP</th>
      <td>India</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>USA</td>
      <td>8</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>Russia</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>China</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>India</td>
      <td>80</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>USA</td>
      <td>90</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>Russia</td>
      <td>89</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>China</td>
      <td>87</td>
    </tr>
    <tr>
      <th rowspan="8" valign="top">2015</th>
      <th>GDP</th>
      <td>India</td>
      <td>6</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>USA</td>
      <td>7</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>Russia</td>
      <td>8</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>China</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>India</td>
      <td>88</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>USA</td>
      <td>92</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>Russia</td>
      <td>91</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>China</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>



# Crosstab in Pandas


```python
df7
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
      <th>Country</th>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>India</td>
      <td>2010</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>USA</td>
      <td>2010</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Russia</td>
      <td>2010</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>China</td>
      <td>2010</td>
      <td>GDP</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>India</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>USA</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>90</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Russia</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>89</td>
    </tr>
    <tr>
      <th>7</th>
      <td>China</td>
      <td>2010</td>
      <td>Literacy</td>
      <td>87</td>
    </tr>
    <tr>
      <th>8</th>
      <td>India</td>
      <td>2015</td>
      <td>GDP</td>
      <td>6</td>
    </tr>
    <tr>
      <th>9</th>
      <td>USA</td>
      <td>2015</td>
      <td>GDP</td>
      <td>7</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Russia</td>
      <td>2015</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>11</th>
      <td>China</td>
      <td>2015</td>
      <td>GDP</td>
      <td>8</td>
    </tr>
    <tr>
      <th>12</th>
      <td>India</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>88</td>
    </tr>
    <tr>
      <th>13</th>
      <td>USA</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>92</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Russia</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>91</td>
    </tr>
    <tr>
      <th>15</th>
      <td>China</td>
      <td>2015</td>
      <td>Literacy</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.crosstab(df7['Literacy/GDP'] , df7.Value , margins=True)
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
      <th>Value</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>80</th>
      <th>87</th>
      <th>88</th>
      <th>89</th>
      <th>90</th>
      <th>91</th>
      <th>92</th>
      <th>93</th>
      <th>All</th>
    </tr>
    <tr>
      <th>Literacy/GDP</th>
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
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>GDP</th>
      <td>2</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>8</td>
    </tr>
    <tr>
      <th>All</th>
      <td>2</td>
      <td>3</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 2 way cross table
pd.crosstab(df7.Year , df7['Literacy/GDP'] , margins=True)
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
      <th>Literacy/GDP</th>
      <th>GDP</th>
      <th>Literacy</th>
      <th>All</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010</th>
      <td>4</td>
      <td>4</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>4</td>
      <td>4</td>
      <td>8</td>
    </tr>
    <tr>
      <th>All</th>
      <td>8</td>
      <td>8</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 3 way cross table
pd.crosstab([df7.Year , df7['Literacy/GDP']] , df7.Country, margins=True)
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
      <th>Country</th>
      <th>China</th>
      <th>India</th>
      <th>Russia</th>
      <th>USA</th>
      <th>All</th>
    </tr>
    <tr>
      <th>Year</th>
      <th>Literacy/GDP</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">2010</th>
      <th>GDP</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2015</th>
      <th>GDP</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Literacy</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>All</th>
      <th></th>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>



# Row & Column Bind

### Row Bind


```python
df8 = pd.DataFrame({'ID' :[1,2,3,4] ,  'Name' :['Murilo' , 'Krominski' , 'Ross' , 'John'] , 'Score' :[99 , 66 , 44 , 33]})
df8
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
      <th>ID</th>
      <th>Name</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
      <td>99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Ross</td>
      <td>44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
      <td>33</td>
    </tr>
  </tbody>
</table>
</div>




```python
df9 = pd.DataFrame({'ID' :[5,6,7,8] ,  'Name' :['Michelle' , 'Ramiro' , 'Vignesh' , 'Damon'] , 'Score' :[78 , 54 , 77 , 87]})
df9
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
      <th>ID</th>
      <th>Name</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>Michelle</td>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>Ramiro</td>
      <td>54</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>Vignesh</td>
      <td>77</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>Damon</td>
      <td>87</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Row Bind with concat() function
pd.concat([df8 , df9])
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
      <th>ID</th>
      <th>Name</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
      <td>99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Ross</td>
      <td>44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
      <td>33</td>
    </tr>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>Michelle</td>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>Ramiro</td>
      <td>54</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>Vignesh</td>
      <td>77</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>Damon</td>
      <td>87</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Row Bind with append() function
df8.append(df9)
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
      <th>ID</th>
      <th>Name</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
      <td>99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Ross</td>
      <td>44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
      <td>33</td>
    </tr>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>Michelle</td>
      <td>78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>Ramiro</td>
      <td>54</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>Vignesh</td>
      <td>77</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8</td>
      <td>Damon</td>
      <td>87</td>
    </tr>
  </tbody>
</table>
</div>



### Column Bind


```python
df10 = pd.DataFrame({'ID' :[1,2,3,4] , 'Name' :['Murilo' , 'Krominski' , 'Ross' , 'John']})
df10
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
      <th>ID</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Ross</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
    </tr>
  </tbody>
</table>
</div>




```python
df11 = pd.DataFrame({'Age' :[20,30,35,40] , 'Score' :[99 , 66 , 44 , 33]})
df11
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
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>30</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>35</td>
      <td>44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>40</td>
      <td>33</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([df10,df11] , axis = 1)
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
      <th>ID</th>
      <th>Name</th>
      <th>Age</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Murilo</td>
      <td>20</td>
      <td>99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Krominski</td>
      <td>30</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Ross</td>
      <td>35</td>
      <td>44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>John</td>
      <td>40</td>
      <td>33</td>
    </tr>
  </tbody>
</table>
</div>


