---
title: Python Source
date: 2019-08-19 14:33:00
categories:
- Python
tags:
- Python
thumbnail: https://user-images.githubusercontent.com/42334717/63241394-80967780-c28e-11e9-939d-2cf7d397c2ec.png
---
# Class def

~~~Python
class 클래스 이름:
    def __init__(self, parm, ...):
        ...
    def method1(self, parm, ...):
        ...
    def method2(self, parm, ...):
        ...
~~~

<!-- more -->
***
# Numpy

+ `import numpy as np`
+ `np.array`로 N차원 배열 가능
***
# Graph plot

~~~Python
import numpy as np
import matplotlib.pyplot as plt

x=np.arange(0,6,0.1)
y1=np.sin(x)
y2=np.cos(x)

plt.plot(x,y1,label="sin")
plt.plot(x,y2,linestyle="--",label="cos")
plt.xlabel("x")
plt.ylabel("y")
plt.title('sin & cos')
plt.legend()
plt.show()
~~~

![](https://user-images.githubusercontent.com/42334717/63241598-44174b80-c28f-11e9-97d5-53dfaca9acaf.png)
***
# Image plot

~~~Python
import matplotlib.pyplot as plt
from matplotlib.image import imread

img = imread('wallpaper.png')

plt.imshow(img)
plt.show()
~~~

![](https://user-images.githubusercontent.com/42334717/63241394-80967780-c28e-11e9-939d-2cf7d397c2ec.png)
***
# 퍼셉트론으로 XOR def

~~~Python
def XOR(x1,x2):
    s1=NAND(x1,x2)
    s2=OR(X1,x2)
    y=AND(s1,s2)
    return y
~~~