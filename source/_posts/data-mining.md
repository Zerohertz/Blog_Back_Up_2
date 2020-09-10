---
title: Data Mining
date: 2020-02-06 14:24:06
categories:
- Book
- Data Mining
tags:
- Machine Learning
- DNN
- Signal Processing
- Statistics
mathjax: true
---
# Introduction

## Why Data Mining?

> 데이터가 풍부하지만 정보가 열악한 상황 - 강력한 데이터 분석 도구 필요

+ Repository에 수집 및 저장되는 크고 많은 데이터 빠르게 성장하는 빅데이터는 강력한 도구 없이는 이해할 수 없음
+ 결과적으로 빅데이터 Repository에서 수집된 데이터는 거의 방문하지 않는 데이터 Archive인 데이터 무덤이 됨
+ 의사 결정자에게 방대한 양의 데이터에 포함된 지식 추출 도구가 없기 때문에 데이터 Repository에 저장된 정보가 풍부한 데이터가 아니라 의사 결정자의 직감에 따라 중요한 의사결정이 종종 이루어짐
+ 이를 위해 수동 지식 입력을 해야하지만 편견과 오류가 발생하기 쉽고 비용이 많이 들며 시간이 많이 걸림
+ **그러므로 데이터 마이닝 도구를 체계적으로 개발해야함**

## Data Mining?

> 데이터를 통해 지식을 캐냄

1. Data cleaning(노이즈 및 일관되지 않은 데이터 제거)
2. Data integration(여러 데이터 소스를 결합할 수 있는 경우)
3. Data selection(분석 작업과 관련된 데이터를 데이터 베이스에서 검색)
4. Data transformation(요약 또는 집계 후 데이터 마이닝에 적합한 형태로 변환 및 통합되는 경우)
5. **Data mining**(데이터 패턴 추출에 지능적인 방법을 적용하는 필수 프로세스)
6. Pattern evaluation(측정에 기초하여 지식을 나타내는 패턴 식별)
7. Knowledge presentation(시각화 및 지식 표현 기술을 사용하여 사용자에게 채굴한 지식을 제시)

## What kinds of Data Can Be Mined?

+ Database data
  + Database management system(DBMS)라고도 불림
  + 상호 관련된 데이터 모음
  + Relational database
    + Attributes(Columns or Fields)
    + Tuples(Records or Rows)
    + Database queries를 통하여 접근할 수 있음
+ Data warehouse
  + 여러 소스에서 수집되어 통합 스키마로 저장
  + 일반적으로 단일 사이트에있는 정보의 저장소
  + Data cleaning, Data integration, Data transformation, Data loading, Periodic data refreshing을 통하여 구성
  + 다차원적인 데이터 구조인 Data cube를 통하여 모델링됨
    + 각 차원은 스키마의 Attribute 또는 Attribute의 집합에 해당
    + 각 셀은 집계 측정 값을 저장
+ Other Kinds of Data
  + Transactional data
  + Time-related or sequence data
  + Data streams
  + Spatial data
  + Engineering design data
  + Hypertext and multimedia data
  + Graph and networked data
  + Web

<!-- More -->

## What kinds of Patterns Can Be Mined?

+ Class/Concept Description
  + Data characterization : A Summarization of the general characteristics or features of a target class of data
  + Data discrimination : A comparison of the general features of the target class data objects against the general features of objects from one or multiple contrasting classes
+ Mining Frequent Patterns, Associations, and Correlations
  + Association analysis

## Analysis of Data

### Classification

> The process of finding a model(or function) that describes and distinguishes data classes or concepts

+ 모델은 훈련 데이터의 분석을 기반하여 파생
+ 모델은 Data를 Class label로 식별
+ Example
  + Decision tree
  + Neural network
+ Regression
  + 연속값 함수를 모델링
  + 누락되거나 사용할 수 없는 데이터 예측

### Cluster Analysis

> Clustering analyzes data objects without consulting class labels

### Outlier Analysis

> Outliers may be detected using statiscal tests that assume a distribution or probability model for the data, or using distance measures where objects that are remote from any other clustrerare considered outliers

***

# Getting to Know Your Data

## Data objects and Attribute Types

+ Data object : Representing an entity, The row of a database
+ Data tuple : If the data objects are stored in a database
+ Attribute : The columns of a database

### What Is an Attribute?

> An attribute is a data field, representing a characteristic or feature of a data object

+ Nominal(명사의) Attributes : The values of a nominal attribute are symbols or names of things
+ Binary Attributes : A binary attribute is a nominal attribute with only two categories or states : 0 or 1, where 0 typically means that the attribute is absent, and 1 means that it is present
+ Ordinal(서수) Attributes : An ordinal attribute is an attribute with possible with possible values that have a meaningful order or ranking among them, but the magnitude between successive values is not known
+ Numeric Attributes : A numeric attribute is quantitative

### Discrete versus Continuous Attributes

+ A discrete attribute has a finite or countably infinite set of values, which may or may not be represented as integers
+ If an attribute is not discrete, it is continuous

## Basic Statistical Descriptions of Data

### Measuring the Central Tendency : Mean, Median, and Mode

+ Mean
$$\bar x = \frac{\sum_{i=1}^{N} x_i}{N}=\frac{x_1+x_2+...+x_N}{N}$$

+ Weighted arithmetic mean / Weighted average
$$\bar x=\frac{\sum_{i=1}^{N}w_ix_i}{\sum_{i=1}^{N}w_i}=\frac{w_1x_1+w_2x_2+...+w_Nx_N}{w_1+w_2+...+w_N}$$

+ Median
  + $L_1$ : The lower boundary of the median interval
  + $N$ : The number of values in the entire data set
  + $(\sum freq)_l$ : The sum of the frequencies of all the intervals that are lower than the median interval
  + $freq_{median}$ : The frequency of the median interval
  + $width$ : The width of the median interval

$$median=L_1+(\frac{N/2-(\sum freq)}{freq_{median}})width$$

+ Mode : A set of data is the value that occurs most frequently in the set
  + Unimodal
  + Bimodal
  + Trimodal
  + Multimodal

![Skewness](https://user-images.githubusercontent.com/42334717/74623830-798eea00-5189-11ea-9b92-2a254b4bbb79.png)

### Measuring the Dispersion of Data : Range, Quartiles, Variance, Standard Deviation, and Interquartile Range

#### Range, Quartiles, and Interquartile Range

+ Range
  + The difference between the largest(`max()`) and smallest(`min()`) values
+ Quartiles
  + Points taken at regular intervals of a data distribution, dividing it into essentially equal size consecutive sets
+ Percentiles
  + The 100-quartiles
+ First quartile
  + $Q_1$, 25th percentile
+ Third quartile
  + $Q_3$, 75th percentile
+ Interquartile range(IQR)
  + $IQR=Q_3-Q_1$

![Percentile](https://user-images.githubusercontent.com/42334717/74625699-8d8a1a00-5190-11ea-8bd3-2b3e2b76f36b.png)

#### Five-Number Summary, Boxplots, and Outliers

+ Five-Number Summary
  + Minimum
  + $Q_1$
  + Median($Q_2$)
  + $Q_3$
  + Maximum

~~~R
> summary(Cars93$Price)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   7.40   12.20   17.70   19.51   23.30   61.90 
~~~

+ Boxplots
  + Typically, the ends of the box quartiles so that the box length is the interquartile range(IQR)
  + The median is marked by a line within the box
  + Two lines(called whiskers) outside the box extend to the smallest(Minimum) and largest(Maximum) observations

~~~R
> boxplot(Cars93$Price)
~~~

<img width="1145" alt="Boxplot" src="https://user-images.githubusercontent.com/42334717/74628030-dc877d80-5197-11ea-8101-600f431aca58.png">

#### Variance and Standard Deviation

+ Variance
$$\sigma^2=\frac{1}{N}\sum_{i=1}^{N}(x_i-\bar x)^2=(\frac{1}{N}\sum_{i=1}^{N}x_i^2)-\bar x^2$$

+ Standard deviation
$$\sigma$$

### Graphic Displays of Basic Statistical Descriptions of Data

+ Quantile Plot
+ Quantile-Quantile Plot(q-q plot)
+ Histograms(frequency histograms)
+ Scatter Plots
+ Data Correlation

## Data Visualization

> Data visualization aims to communicate data clearly and effectively through graphical representation

### Pixel-Oriented Visualization Techniques

+ For a data set of m dimensions, pixel-oriented techniques create m windows on the screen, one for each dimension
+ The m dimension values of a record are mapped to m pixels at the corresponding positions in the windows
+ The colors of the pixels reflect the corresponding values

![Pixel-Oriented Visualization Techniques](https://user-images.githubusercontent.com/42334717/74633998-532b7780-51a6-11ea-859a-33193cf8f4f0.png)

### Geometric Projection Visualization Techniques

> Geometric projection techniques help users find interesting projections of multidimensional data sets

![Geometric Projection Visualization Techniques](https://user-images.githubusercontent.com/42334717/74634132-9ede2100-51a6-11ea-8a94-2887f8e3d463.png)

### Icon-Based Visualization Techniques

> Icon-based visualization techniques use small icons to represent multidimensional data values

![Icon-Based Visualization Techniques](https://user-images.githubusercontent.com/42334717/74634337-fa101380-51a6-11ea-8ba2-13030ecf6be7.png)

### Hierarchical Visualization Techniques

> Hierarchical Visualization Techniques partition all dimensions into subsets

## Measuring Data Similarity and Dissimilarity

> In data mining applications, such as clustering, outlier analysis, and nearest-neighbor classification, we need ways to assess how alike or unalike objects are in comparison to one another

### Data Matrix versus Dissimilarity Matrix

+ Data matrix(or $object-by-attribute structure$)
  + This structure stores the $n$ data objects in the form of a relational table
  + $n-by-p$ matrix
  + $n\ objects\ \times\ p\ attributes$

$$
\begin{bmatrix}{}
x_{11} & \ldots & x_{1f} & \ldots & x_{1p} \\\\
\ldots & \ldots & \ldots & \ldots & \ldots \\\\
x_{i1} & \ldots & x_{if} & \ldots & x_{ip} \\\\
\ldots & \ldots & \ldots & \ldots & \ldots \\\\
x_{n1} & \ldots & x_{nf} & \ldots & x_{np} \\\\
\end{bmatrix}
$$

+ Dissimilarity matrix(or $object-by-object structure$)
  + This structure stores a collection of proximities that are available for all pairs of $n$ objects
  + $n-by-n$ table
  + $d(i,j)$ : The measured dissimilarity or difference between objects $i$ and $j$
  + In general, $d(i,j)$ is a non-negative number that is close to 0 when objects $i$ and $j$ are highly similar or near each other, and becomes larger the more they differ
  + $d(i,j)=d(j,i)$

$$
\begin{bmatrix}{}
0 \\\\
d(2,1) & 0 \\\\
d(3,1) & d(3,2) & 0 \\\\
\vdots & \vdots & \vdots \\\\
d(n,1) & d(n,2) & \ldots & \ldots & 0 \\\\
\end{bmatrix}
$$


+ The similarity between objects $i$ and $j$

$$sim(i,j)=1-d(i,j)$$

+ Data matrix : Two-mode matrix(Two entities or things, namely rows(for objects) and columns(for attributes))
+ Dissimilarity matrix : One-mode matrix(One kind of entity(dissimilarities))

### Proximity Measures for Nominal Attribute

+ The dissimilarity between two objects $i$ and $j$
  + $m$ : The number of matches
  + $p$ : The total number of attributes describing the objects
  + Weights can be assigned to increase the effect of $m$ or to assign greater weight to the matches in attributes having a larger number of states

$$d(i,j)=\frac{p-m}{p}$$

+ The similarity
$$sim(i,j)=1-d(i,j)=\frac{m}{p}$$

### Proximity Measures for Binary Attributes

![Binary Attributes Table](https://user-images.githubusercontent.com/42334717/74701775-3a28d200-524b-11ea-8608-41c177e88e74.png)

$$p=q+r+s+t$$

+ Symmetric binary dissimilarity
$$d(i,j)=\frac{r+s}{q+r+s+t}$$

+ Asymmetric binary dissimilarity
  + $t$ is considered unimportant and is thus ignored in the following computation
$$d(i,j)=\frac{r+s}{q+r+s}$$

+ Asymmetric binary similarity
$$sim(i,j)=\frac{q}{q+r+s}=1-d(i,j)$$

### Dissimilarity of Numeric Data : Minkowski Distance

+ Euclidean distance
$$d(i,j)=\sqrt{(x_{i1}-x_{j1})^2+(x_{i2}-x_{j2})^2+...+(x_{ip}-x_{jp})^2}$$

+ Mangattan(or city block) distance
$$d(i,j)=|x_{i1}-x_{j1}|+|x_{i2}-x_{j2}|+...+|x_{ip}-x_{jp}|$$


+ Both the Euclidean and the Manhattan distance satisfy the following mathematical properties
  + Non-negativity : $d(i,j)\geq0$ : Distance is a non-negative number
  + Identity of indiscernibles : $d(i,i)=0$ : The distance of an object to itself is 0
  + Symmertry : $d(i,j)=d(j,i)$ : Distance is a symmetric function
  + Triangle inequality : $d(i,j)\leq d(i,k)+d(k,j)$ : Going directly from object $i$ to object $j$ in space is no more than making a detour over any other object $k$


+ The supremum distance($L_{max},\ L_{\infty}\ norm,\ Chebyshev\ distance$)
  + A generalization of the Minkowski distance for $h\to \infty$
$$d(i,j)=\lim_{h\to \infty}(\sum_{f=1}^p|x_{if}-x_{jf}|^h)^{\frac{1}{h}}=\max_f^p|x_{if}-x_{jf}|$$

![Distance](https://user-images.githubusercontent.com/42334717/74702739-39de0600-524e-11ea-96a9-7d57e679845a.png)

### Proximity Measures for Ordinal Attributes

+ $M$ : Represent the number of possible states that an ordinal attribute can have
+ $f$ : An attribute from a set of ordinal attributes describing $n$ objects

1. The value of $f$ for the $i$th object is $x_{if}$, and $f$ has $M_f$ ordered states, representing the ranking $1,...,M_f$. Replace each $x_{if}$ by its corresponding rank, $r_{if}\in\{1,...,M_f\}$
2. Since each ordinal attribute can have a different number of sstates, it is often necessary to map the range of each attribute onto $[0.0,\ 1.0]$ so that each attribute has equal weight. We perform such data normalization by replacing the rank $r_{if}$ of the $i$th object in the $f$th attribute by
$$z_{if}=\frac{r_{if}-1}{M_f-1}$$
3. Dissimilarity can then be computed using any of the distance measures, using $z_{if}$ to represent the $f$ value for the $i$th object.

### Dissimilarity for Attributes of Mixed Types

+ The dissimilarity $d(i,j)$ between objects $i$ and $j$
  + The data set contains $p$ attributes of mixed type
  + The indicator $\delta_{ij}^{(f)}$
    + $\delta_{ij}^{(f)}=0$
      1. $x_{if}$ or $x_{jf}$ is missing
      2. $x_{if}=x_{jf}=0$ and attribute $f$ is asymmetric binary
    + $\delta_{ij}^{(f)}=1$
      + The contribution of attribute $f$ to the dissimilarity between $i$ and $j$(i.e., $d_{ij}^{(f)}$) is computed dependent on its type:
        1. If $f$ is numeric : $d_{ij}^{(f)}=\frac{|x_{if}-x_{jf}|}{\max_hx_{hf}-\min_hx_{hf}}$, where $h$ runs over all nonmissing objects for attribute $f$
        2. If $f$ is nominal or binary : $d_{ij}^{(f)}=0$ if $x_{if}=x_{jf}$; otherwise, $d_{if}^{(f)}=1$
        3. If $f$ is ordinal : compute the ranks $r_{if}$ and $z_{if}=\frac{r_{if}-1}{M_f-1}$, and treat $z_{if}$ as numeric
$$d(i,j)=\frac{\sum_{f=1}^p \delta_{ij}^{(f)}d_{ij}^{(f)}}{\sum_{f=1}^p \delta_{ij}^{(f)}}$$

### Cosine Similarity

Term-frequency vector : Each document is an object represented(Typically very long and sparse)

+ Similarity function
  + Measure of similarity that can be used to compare documents or, say, give a ranking of documents with respect to a given vector of query words
  + $\boldsymbol{x},\ \boldsymbol{y}$ : Two vectors for comparision
  + $||\boldsymbol{x}||$ : Euclidean norm of vector $\boldsymbol{x}=(x_1,x_2,...,x_p)$
  + $||\boldsymbol{y}||$ : Euclidean norm of vector $\boldsymbol{y}=(y_1,y_2,...,y_p)$
  + A cosine value of 0 means that the two vectors are at 90 degrees to each other (orthognal) and have no match
  + The closer the cosine value of 1, the smaller the angle and the greater the match between vectors
$$sim(\boldsymbol{x},\boldsymbol{y})=\frac{\boldsymbol{x}\cdot \boldsymbol{y}}{||\boldsymbol{x}||||\boldsymbol{y}||}$$

+ Tanimoto coefficient(or Tanimoto distance)
  + When attributes are binary-valued, the cosine similarity function can be interpreted in terms of shared features or attributes
  + The ratio of the number of attributes shared by $\boldsymbol{x}$ and $\boldsymbol{y}$ to the number of attributes possessed by $\boldsymbol{x}$ or $\boldsymbol{y}$
$$sim(\boldsymbol{x},\boldsymbol{y})=\frac{\boldsymbol{x}\cdot \boldsymbol{y}}{\boldsymbol{x}\cdot \boldsymbol{x}+\boldsymbol{y}\cdot \boldsymbol{y}-\boldsymbol{x}\cdot \boldsymbol{y}}$$

***

# Data Preprocessing

1. Data Cleaning
2. Data Integration
3. Data Reduction
4. Data Transformation

![Data Processing](https://user-images.githubusercontent.com/42334717/89777041-f487fa80-db45-11ea-9dc4-f9a644fb68b9.png)

+ 데이터 품질을 결정하는 요소
  + 정확성
  + 완전성
  + 일관성
  + 적시성
  + 신뢰성
  + 해석 가능성

## Data Cleaning

### Missing Values

1. Ignore the tuple
2. Fill in the missing value manually
3. Use a global constant to fill in the missing value
4. Use a measure of central tendency for the attribute to fill in the missing value
5. Use the attribute mean or median for all samples belonging to the same class as the given tuple
6. Use the most probable value to fill in the missing value

### Noisy Data

> Noise is a random error or variance in a measured variable

> Binning : Binning methods smooth a sorted data value by consulting its "neighbor-hood" that is, the values around it.

+ Smoothing by bin means
+ Smoothing by bin medians
+ Smoothing by bin boundaries
+ Regression
+ Outlier analysis

### Data Cleaning as a Process

> As we discover more about the data, it is important to keep updating the metadata to reflect this knowledge

## Data Integration

> Data mining often requires data integration - the merging of data from multiple data stores

### Redundancy and Correlation Analysis

> Some redundancies can be detected by correlation analysis

#### $\chi^2$ Correlation Test for Nominal Data

> For nominal data, a correlation relationship between two attributes, A and B, can be discovered by a $\chi^2$(chi-square) test

+ The $\chi^2$ value(also known as the $Pearson\ \chi^2\ statistic$)
  + A has $c$ distinct values, namely $a_1, a_2, ..., a_c$
  + B has $r$ distinct values, namely $b_1, b_2, ..., b_r$
  + The data tuples described by A and B can be shown as  a contingency table, with the $c$ values of A making up the columns and the $r$ values of B making up the rows
  + Let $(A_i,B_j)$ denote the joint event that attribute A takes on value $a_i$ and attribute B takes on value $b_j$, that is, where $(A=a_i,B=b_j)$

$$\chi^2=\sum_{i=1}^c\sum_{j=1}^r\frac{(o_{ij}-e_{ij})^2}{e_{ij}}$$

+ $e_{ij}$ : The expected frequency of $(A_i,B_j)$
  + $o_{ij}$ : The observed frequency(i.e., actual count) of the joint event $(A_i,B_j)$
  + n : The number of data tuples
  + $count(A=a_i)$ : The number of tuples having value $a_i$ for A
  + $count(B=b_i)$ : The number of tuples having value $b_i$ for B

$$e_{ij}=\frac{count(A=a_i)\times count(B=b_j)}{n}$$

+ The $\chi^2$ statistics tests the hypothesis that A and B are independent, that is, there is no correlation between them
+ The test is based on a significance level, with $(r-1)\times (c-1)$ degrees of freedom
+ If the hypothesis can be rejected, then we say that A and B are statistically correlated

#### Correlation Coefficient for Numeric Data

+ The correlation coefficient(Pearson's product moment coefficient)
  + $n$ : The number of tuples
  + $a_i$ : The value of A in tuple $i$
  + $b_i$ : The value of B in tuple $j$
  + $\bar A$ : The mean value of A
  + $\bar B$ : The mean value of B
  + $\sigma_A$ : The standard deviation of A
  + $\sigma_B$ : The standard deviation of B
  + $\sum(a_ib_i)$ : The sum of the AB cross-product
  + $-1\leq r_{A,B}\leq+1$
  + If $r_{A,B}$ is greater than 0, then A and B are positively correlated
  + Hence, a higher value may indicate that A (or B) may be removed as a redundancy
  + If the resulting value is equal to 0, then A and B are independent and there is no correlation between them
  + If the resulting value is less than 0, then A and B are negatively correlated, where the values of one attribute increase as the values of the other attribute decrease
  + Scatter plots can also be used to view correlations between attributes

$$r_{A,B}=\frac{\sum_{i=1}^n(a_i-\bar A)(b_i-\bar B)}{n\sigma_A\sigma_B}=\frac{\sum_{i=1}^n(a_ib_i)-n\bar A\bar B}{n\sigma_A\sigma_B}$$

#### Covariance of Numeric Data

+ The mean values of A and B, respectively, are also known as the expected values on A and B

$$E(A)=\bar A=\sum_{i=1}^na_i$$

$$E(B)=\bar B=\sum_{i=1}^nb_i$$

+ Covariance
  + In probability theory and statistics, correlation and covariance are two similar measures for assessing how much two attributes change together
  + For two attributes A and B that tend to change together, if A is larger than $\bar A$, then B is likely to be larger than $\bar B$
  + Therefore, the covariance between A and B is positive
  + On the other hand, if one of the attributes tends to be above its expected value when the other attribute is below its expected value, then the covariance of A and B is negative
  + If A and B are independent(i.e., they do not have correlation), then $E(A\cdot B)=E(A)\cdot E(B)$
  + Therefore, the covariance is $Cov(A,B)=E(A\cdot B)-\bar A\bar B=E(A)\cdot E(B)-\bar A\bar B=0$
  + However, the converse is not true
  + Some pairs of random variables(attributes) may have a covariance of 0 but are not independent

$$
Cov(A,B)=E((A-\bar A)(B-\bar B))=\frac{\sum_{i=1}^n(a_i-\bar A)(b_i-\bar B)}{n}
$$
$$
Cov(A,B)=E(A\cdot B)-\bar A\bar B
$$

+ $r_{A,B}$(Correlation coefficient)
  + for covariance

$$
r_{A,B}=\frac{Cov(A,B)}{\sigma_A\sigma_B}
$$

+ Standard deviations of A and B, respectively
  + $\sigma_A$
  + $\sigma_B$

### Tuple Duplication

> In addition to detecting redundancies between attributes, duplication should also be detected at the tuple level

+ The use of denormalized tables(often done to improve performance by avoiding joins) is another source of data redundancy
+ Inconsistencies often arise between various duplicates, due to inaccurate data entry or updating some but not all data occurences

### Data Value Conflict Detection and Resolution

> Data integration also involves the detection and resolution of data value conflicts

+ Differences in representation
+ Scaling
+ Encoding

## Data Reduction

> Data reduction techniques can be applied to obtain a reduced representation of the data set that is much smaller in volume, yet closely maintains the integrity of the original data

### Overview of Data Reduction Strategies

+ Dimensionality reduction
  + The process of reducing the number of random variables or attributes under consideration
+ Numerosity reduction
  + The techniques replace the original data volume by alternative, smaller forms of data representation
+ Data compression
  + Transformations are applied so as to obtain a reduced or "compressed" representation of the original data


**The computational time spent on data reduction should not out weigh or "erase" the time saved by mining on a reduced data set size**

### Wavelet Transform

> The discrete wavelet transform(DWT) is a linear signal processing technique that, when applied to a data vector **X**, transforms it to a numerically different vector, **X'**, of wavelet coefficients

+ Consider each tuple as an $n$-dimensional data vector
  + **$X$**$=(x_1,x_2,...,x_n)$
  + Depicting $n$ measurements made on the tuple from $n$ database attributes
+ The DWT is closely related to the discrete Fourier transform(DFT)
  + DFT : A signal processing technique involving sines and cosines

### Principal Components Analysis(PCA)

> 데이터를 표현하는데 가장 잘 사용할 수 있는 직교 벡터 분석

+ 정렬된 속성과 정렬되지 않은 속성에 적용할 수 있음
+ 희소 데이터와 치우친 데이터를 처리할 수 있음
+ 2차원 이상의 다차원 데이터는 문제를 2차원으로 줄여 처리
+ 웨이블릿 변환과 비교 시 PCA는 희소 데이터를 처리하는데 더 나은 경향이 있는 반면, 웨이블릿 변환은 고차원 데이터에 더 적합

### Attribute Subset Selection

> 관련이 없거나 중복된 속성(또는 차원)을 제거하여 데이터의 크기를 줄임

+ 데이터 클래스의 결과 확률 분포가 모든 속성을 사용하여 얻은 원래 분포에 최대한 가깝도록 속성의 최소 집합을 찾음
+ 검색된 패턴에 나타나는 속성의 수를 줄여 패턴을 이해하기 쉽게 만듦

### Regression and Log-Linear Models : Parametric Data Reduction

> Regression and log-linear models can be used to approximate the give data

$$
y=\omega x+b
$$

+ $y$ : Respoonse variable
+ $x$ : Predictor variable
+ $\omega ,b$ : Regression coefficients