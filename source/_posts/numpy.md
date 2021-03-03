---
title: Numpy
date: 2021-02-28 16:12:55
categories:
- Python
tags:
- Machine Learning
- DNN
- Statistics
- Python
mathjax: true
---
{% gdemo_terminal 'import numpy as np' '60px' 'python' '300' '> ' 'python' 'python' %}
{% endgdemo_terminal %}

<!-- More -->

# Initialize

## 0으로 초기화

~~~python init_zero.py
import numpy as np

a = np.zeros(5)
b = np.zeros((5,4))

print('a = ', a)
print('********************')
print('b = ', b)
print('********************')

print('b.shape = ', b.shape)
print('********************')
print('b.ndim', b.ndim) #len(b.shape)
print('********************')
print('b.size = ', b.size)
~~~

~~~python Result
a =  [0. 0. 0. 0. 0.]
********************
b =  [[0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]]
********************
b.shape =  (5, 4)
********************
b.ndim 2
********************
b.size =  20
~~~

## 1로 초기화

~~~python init_one.py
import numpy as np

a = np.ones(5)
b = np.ones((5,4))

print('a = ', a)
print('********************')
print('b = ', b)
~~~

~~~python Result
a =  [1. 1. 1. 1. 1.]
********************
b =  [[1. 1. 1. 1.]
 [1. 1. 1. 1.]
 [1. 1. 1. 1.]
 [1. 1. 1. 1.]
 [1. 1. 1. 1.]]
~~~

## 지정한 수로 초기화

~~~python init_sel.py
import numpy as np

a = np.full(5, 42)
b = np.full((5,4), 21)

print('a = ', a)
print('********************')
print('b = ', b)
~~~

~~~python Result
a =  [42 42 42 42 42]
********************
b =  [[21 21 21 21]
 [21 21 21 21]
 [21 21 21 21]
 [21 21 21 21]
 [21 21 21 21]]
~~~

## List로 초기화

~~~python init_list.py
import numpy as np

a = np.array([10, 10, 10])
b = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

print('a = ', a)
print('********************')
print('b = ', b)
print('********************')
print('Type of b = ', type(b))
~~~

~~~python Result
a =  [10 10 10]
********************
b =  [[1 2 3]
 [4 5 6]
 [7 8 9]]
********************
Type of b =  <class 'numpy.ndarray'>
~~~

## 범위로 초기화

~~~python init_ran.py
import numpy as np

a = np.arange(0, np.pi, 0.4) #간격의 크기
b = np.linspace(0, np.pi, 6) #간격의 수

print('a = ', a)
print('********************')
print('b = ', b)
~~~

~~~python Result
a =  [0.  0.4 0.8 1.2 1.6 2.  2.4 2.8]
********************
b =  [0.         0.62831853 1.25663706 1.88495559 2.51327412 3.14159265]
~~~

## 함수로 초기화

~~~python init_func.py
import numpy as np

def init_function_2(x, y):
    return x * y

def init_function_3(z, x, y):
    return x * y + z

a = np.fromfunction(init_function_2, (5, 5))
b = np.fromfunction(init_function_3, (2, 5, 5))

print('a = ', a)
print('********************')
print('b = ', b)
~~~

~~~python Result
a =  [[ 0.  0.  0.  0.  0.]
 [ 0.  1.  2.  3.  4.]
 [ 0.  2.  4.  6.  8.]
 [ 0.  3.  6.  9. 12.]
 [ 0.  4.  8. 12. 16.]]
********************
b =  [[[ 0.  0.  0.  0.  0.]
  [ 0.  1.  2.  3.  4.]
  [ 0.  2.  4.  6.  8.]
  [ 0.  3.  6.  9. 12.]
  [ 0.  4.  8. 12. 16.]]

 [[ 1.  1.  1.  1.  1.]
  [ 1.  2.  3.  4.  5.]
  [ 1.  3.  5.  7.  9.]
  [ 1.  4.  7. 10. 13.]
  [ 1.  5.  9. 13. 17.]]]
~~~

## 데이터 형 지정

~~~python data_type.py
import numpy as np

a = np.arange(1, 5, dtype = np.uint8)
b = np.array([[1, 2, 3], [4, 5, 6]], dtype = np.complex64)

print('a = ', a)
print('********************')
print('b = ', b)
~~~

~~~python Result
a =  [1 2 3 4]
********************
b =  [[1.+0.j 2.+0.j 3.+0.j]
 [4.+0.j 5.+0.j 6.+0.j]]
~~~

***

# Methods of np.ndarray

~~~python method_st.py
import numpy as np

a = np.array([[1, 2, 3], [4, 5, 6]], dtype = np.uint8)

for func in (a.shape, a.min, a.max, a.sum, a.prod, a.std, a.var):
    print(func.__name__, "=", func())
~~~

~~~python Result
min = 1
max = 6
sum = 21
prod = 720
std = 1.707825127659933
var = 2.9166666666666665
~~~