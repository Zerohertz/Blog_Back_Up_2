---
title: Diagnosis Systems with Smart Data for 3D Printer(Introduction)
date: 2020-01-14 11:25:23
categories:
- Research
- Journal
tags:
- Machine Learning
- DNN
- Signal Processing
- Matlab
- PHM
- Statistics
- R
- Smart data
- LabVIEW
mathjax: true
---
# Problem Definition

> Self diagnosis systems for unattended 3D printers

+ 다수의 3D printer를 고장났는지 Classification하고 Bolt의 풀림에 따른 고장 Detection System 개발

## 왜도, 첨도, RMS 보다 좋은 Smart Data 추출

## 현재의 3D Printer에 최적화 된 ML Model 개발

***

# Skills for project

+ LabView
+ MatLab
+ Signal Processing
+ Machine Learning
+ Deep Learning

<!-- More -->

***

# RMS

> $$RMS(t)=\sqrt{\frac{1}{N}\sum_{n=t}^{t+winsiz}x_n^2}$$

~~~R
accrms=function(a,b,winsiz){
	z=1
	sink(b)
	cat('[')
	while(z<=(length(a)-winsiz-10)){
		l=0
		s=0
		while(l<winsiz){
			s=s+a[z+l]^2
			l=l+1
		}
		rms=sqrt(s)/winsiz
		cat(rms,'\t')
		z=z+1
	}
	cat(']')
	sink()
}
~~~

![](https://user-images.githubusercontent.com/42334717/72867819-81db3d00-3d23-11ea-969a-80bc218ba0f2.png)

***

# 1차 시도

## Signal Processing

~~~R
setwd("/Users/zerohertz/Downloads")

No=read.table('test1.txt',sep='	',header=T)
We=read.table('test.txt',sep='	',header=T)

sk=function(x,Winsiz){
	i=1
	sk=0
	while((i+Winsiz)<=length(x)){
		j=1
		sam=0
		while(j<=Winsiz){
			sam[j]=x[i+j]
			j=j+1
		}
		sk[i]<-sum(((sam-mean(sam))^3)/sd(sam)^3)*(1/(Winsiz-1))
		i=i+1
	}
	return(sk)
}

ku=function(x,Winsiz){
	i=1
	ku=0
	while((i+Winsiz)<=length(x)){
		j=1
		sam=0
		while(j<=Winsiz){
			sam[j]=x[i+j]
			j=j+1
		}
		ku[i]<-sum(((sam-mean(sam))^4)/sd(sam)^4)*(1/(Winsiz-1))
		i=i+1
	}
	return(ku)
}

rm=function(x,Winsiz){
	i=1
	rm=0
	while((i+Winsiz)<=length(x)){
		j=1
		sam=0
		while(j<=Winsiz){
			sam[j]=x[i+j]
			j=j+1
		}
		rm[i]<-sqrt(sum(sam^2)/Winsiz)
		i=i+1
	}
	return(rm)
}

MakeData=function(data,Winsiz,cut1,cut2,name){
	X_skew=sk(data$UP_X,Winsiz)
	X_kurt=ku(data$UP_X,Winsiz)
	X_rms=rm(data$UP_X,Winsiz)
	Y_skew=sk(data$UP_Y,Winsiz)
	Y_kurt=ku(data$UP_Y,Winsiz)
	Y_rms=rm(data$UP_Y,Winsiz)
	Z_skew=sk(data$UP_Z,Winsiz)
	Z_kurt=ku(data$UP_Z,Winsiz)
	Z_rms=rm(data$UP_Z,Winsiz)
	all=cbind(X_skew,X_kurt,X_rms,Y_skew,Y_kurt,Y_rms,Z_skew,Z_kurt,Z_rms)
	options(max.print=1000000)
	write.table(all[cut1:cut2,1:9],name,sep='\t',row.names=F)
}

Norm=MakeData(No,100,60000,100000,'Norm.txt')
Wear=MakeData(We,100,80000,120000,'Wear.txt')
~~~

## Machine Learning

### Set Learning Data

~~~Matlab
for i=1:40001;
    Target1(i)={'Normal'};
    Target2(i)={'Wear'};
end

Target=[Target1,Target2];
Kurt_Z=[Norm.Norm_Z_kurt;Wear.Wear_Z_kurt];
Kurt_X=[Norm.Norm_X_kurt;Wear.Wear_X_kurt];
Skew_Z=[Norm.Norm_Z_skew;Wear.Wear_Z_skew];
Skew_X=[Norm.Norm_X_skew;Wear.Wear_X_skew];
RMS_Z=[Norm.Norm_Z_rms;Wear.Wear_Z_rms];
RMS_X=[Norm.Norm_X_rms;Wear.Wear_X_rms];
Target=Target';

LearningData=table(Kurt_Z,Kurt_X,Skew_Z,Skew_X,RMS_Z,RMS_X,Target)
~~~

### SVM(Support Vector Machine)의 결과

~~~Matlab
MakeLearningData(Norm,Wear,400001)

CheckData=MakeCheckData(Norm1,Wear1)
        
GS=Checkfunction(CheckData,GaussSVM);
GSX=Checkfunction(CheckData,GaussSVM_X);
GSZ=Checkfunction(CheckData,GaussSVM_Z);
TS=Checkfunction(CheckData,ThirdSVM);
TSX=Checkfunction(CheckData,ThirdSVM_X);
TSZ=Checkfunction(CheckData,ThirdSVM_Z);
~~~

#### Data plot

<img width="1932" alt="Data plot" src="https://user-images.githubusercontent.com/42334717/73722454-e0fc7100-4769-11ea-9a06-76fe007b082a.png">

#### Gauss SVM with X, Z data

<img width="1932" alt="Gauss SVM" src="https://user-images.githubusercontent.com/42334717/73722471-ee196000-4769-11ea-9af1-f55d7f47d0c3.png">
<img width="1932" alt="Gauss SVM" src="https://user-images.githubusercontent.com/42334717/73722480-f40f4100-4769-11ea-9838-0172b0e471b2.png">

~~~R
> checkfunc(GaussSVM)
Normal Predict with Normal Result : 10001 
 - In percentage :  100 %
Wear Predict with Wear Result : 10001 
 - In percentage :  100 %
Normal Predict with Wear Result : 0 
 - In percentage :  0 %
Wear Predict with Normal Result : 0 
 - In percentage :  0 %
~~~

#### Gauss SVM with X data

<img width="1932" alt="Gauss SVM X" src="https://user-images.githubusercontent.com/42334717/73722491-fa052200-4769-11ea-8339-94ce4b236083.png">
<img width="1932" alt="Gauss SVM X" src="https://user-images.githubusercontent.com/42334717/73722497-fe313f80-4769-11ea-8284-b6cbd6ebd9bd.png">

~~~R
> checkfunc(GaussSVM_X)
Normal Predict with Normal Result : 6344 
 - In percentage :  63.43366 %
Wear Predict with Wear Result : 10001 
 - In percentage :  100 %
Normal Predict with Wear Result : 3657 
 - In percentage :  36.56634 %
Wear Predict with Normal Result : 0 
 - In percentage :  0 %
~~~

#### Gauss SVM with Z data

<img width="1932" alt="Gauss SVM Z" src="https://user-images.githubusercontent.com/42334717/73722525-0f7a4c00-476a-11ea-97fb-a18aff69eaa8.png">
<img width="1932" alt="Gauss SVM Z" src="https://user-images.githubusercontent.com/42334717/73722551-1a34e100-476a-11ea-9b75-aa0e6c5f1191.png">

~~~R
> checkfunc(GaussSVM_Z)
Normal Predict with Normal Result : 8486 
 - In percentage :  84.85151 %
Wear Predict with Wear Result : 7420 
 - In percentage :  74.19258 %
Normal Predict with Wear Result : 1515 
 - In percentage :  15.14849 %
Wear Predict with Normal Result : 2581 
 - In percentage :  25.80742 %
~~~

#### 3rd Order SVM with X, Z data

<img width="1932" alt="3rd SVM" src="https://user-images.githubusercontent.com/42334717/73722568-228d1c00-476a-11ea-9854-6f4e7d42e81f.png">
<img width="1932" alt="3rd SVM" src="https://user-images.githubusercontent.com/42334717/73722570-26b93980-476a-11ea-897a-4dc12a7c15d5.png">

~~~R
> checkfunc(ThirdSVM)
Normal Predict with Normal Result : 6739 
 - In percentage :  67.38326 %
Wear Predict with Wear Result : 10001 
 - In percentage :  100 %
Normal Predict with Wear Result : 3262 
 - In percentage :  32.61674 %
Wear Predict with Normal Result : 0 
 - In percentage :  0 %
~~~

#### 3rd Order SVM with X data

<img width="1932" alt="3rd SVM X" src="https://user-images.githubusercontent.com/42334717/73722597-359fec00-476a-11ea-8612-bdfbd00801f5.png">
<img width="1932" alt="3rd SVM X" src="https://user-images.githubusercontent.com/42334717/73722624-43557180-476a-11ea-80b3-414c5ed96c18.png">

~~~R
> checkfunc(ThirdSVM_X)
Normal Predict with Normal Result : 7519 
 - In percentage :  75.18248 %
Wear Predict with Wear Result : 10001 
 - In percentage :  100 %
Normal Predict with Wear Result : 2482 
 - In percentage :  24.81752 %
Wear Predict with Normal Result : 0 
 - In percentage :  0 %
~~~

#### 3rd Order SVM with Z data

<img width="1932" alt="3rd SVM Z" src="https://user-images.githubusercontent.com/42334717/73722579-2c168400-476a-11ea-9d93-565c5465525b.png">
<img width="1932" alt="3rd SVM Z" src="https://user-images.githubusercontent.com/42334717/73722586-3042a180-476a-11ea-8859-1d082dab46e7.png">

~~~R
> checkfunc(ThirdSVM_Z)
Normal Predict with Normal Result : 1856 
 - In percentage :  18.55814 %
Wear Predict with Wear Result : 8607 
 - In percentage :  86.06139 %
Normal Predict with Wear Result : 8145 
 - In percentage :  81.44186 %
Wear Predict with Normal Result : 1394 
 - In percentage :  13.93861 %
~~~

#### MakeLearningData.m

~~~Matlab
function LearningData=MakeLearningData(Norm,Wear,num)
    for i=1:num
        Target1(i)={'Normal'};
        Target2(i)={'Wear'};
    end
    Target=[Target1,Target2];
    Target=Target';
    Kurt_X=[Norm.X_kurt;Wear.X_kurt];
    Kurt_Y=[Norm.Y_kurt;Wear.Y_kurt];
    Kurt_Z=[Norm.Z_kurt;Wear.Z_kurt];
    Skew_X=[Norm.X_skew;Wear.X_skew];
    Skew_Y=[Norm.Y_skew;Wear.Y_skew];
    Skew_Z=[Norm.Z_skew;Wear.Z_skew];
    RMS_X=[Norm.X_rms;Wear.X_rms];
    RMS_Y=[Norm.Y_rms;Wear.Y_rms];
    RMS_Z=[Norm.Z_rms;Wear.Z_rms];
    LearningData=table(Kurt_X,Kurt_Y,Kurt_Z,Skew_X,Skew_Y,Skew_Z,RMS_X,RMS_Y,RMS_Z,Target);
end
~~~

#### MakeCheckData.m

~~~Matlab
function CheckData=MakeCheckData(Norm,Wear)
    Kurt_X=[Norm.X_kurt;Wear.X_kurt];
    Kurt_Y=[Norm.Y_kurt;Wear.Y_kurt];
    Kurt_Z=[Norm.Z_kurt;Wear.Z_kurt];
    Skew_X=[Norm.X_skew;Wear.X_skew];
    Skew_Y=[Norm.Y_skew;Wear.Y_skew];
    Skew_Z=[Norm.Z_skew;Wear.Z_skew];
    RMS_X=[Norm.X_rms;Wear.X_rms];
    RMS_Y=[Norm.Y_rms;Wear.Y_rms];
    RMS_Z=[Norm.Z_rms;Wear.Z_rms];
    CheckData=table(Kurt_X,Kurt_Y,Kurt_Z,Skew_X,Skew_Y,Skew_Z,RMS_X,RMS_Y,RMS_Z)
end
~~~

#### Checkfunction.m

~~~Matlab
function result=Checkfunction(data,func)
    for k=1:height(data)
        if k>height(data)/2
            z={'Wear'};
        else k<=height(data)/2
            z={'Normal'};
        end
        p=func.predictFcn(data(k,:));
        Predict(k)=p;
        Result(k)=z;
    end
    
    Predict=Predict';
    Result=Result';
    
    result=table(Predict,Result);
end
~~~

#### Result.R

~~~R
setwd("/Users/zerohertz/Downloads")

GaussSVM=read.table('GaussSVM_Result.txt',header=T)
GaussSVM_X=read.table('GaussSVM_X_Result.txt',header=T)
GaussSVM_Z=read.table('GaussSVM_Z_Result.txt',header=T)
ThirdSVM=read.table('ThirdSVM_Result.txt',header=T)
ThirdSVM_X=read.table('ThirdSVM_X_Result.txt',header=T)
ThirdSVM_Z=read.table('ThirdSVM_Z_Result.txt',header=T)

checkfunc=function(data){
	cat('Normal Predict with Normal Result : ')
	Z=nrow(subset(data,subset=((data$Result=='Normal')&(data$Predict=='Normal'))))
	cat(Z,'\n','- In percentage : ',Z/nrow(subset(data,subset=(data$Result=='Normal')))*100,'%\n')
	cat('Wear Predict with Wear Result : ')
	Z=nrow(subset(data,subset=((data$Result=='Wear')&(data$Predict=='Wear'))))
	cat(Z,'\n','- In percentage : ',Z/nrow(subset(data,subset=(data$Result=='Wear')))*100,'%\n')
	cat('Normal Predict with Wear Result : ')
	Z=nrow(subset(data,subset=((data$Result=='Normal')&(data$Predict=='Wear'))))
	cat(Z,'\n','- In percentage : ',Z/nrow(subset(data,subset=(data$Result=='Normal')))*100,'%\n')
	cat('Wear Predict with Normal Result : ')
	Z=nrow(subset(data,subset=((data$Result=='Wear')&(data$Predict=='Normal'))))
	cat(Z,'\n','- In percentage : ',Z/nrow(subset(data,subset=(data$Result=='Wear')))*100,'%\n')
}

checkfunc(GaussSVM)
checkfunc(GaussSVM_X)
checkfunc(GaussSVM_Z)
checkfunc(ThirdSVM)
checkfunc(ThirdSVM_X)
checkfunc(ThirdSVM_Z)
~~~

***

# 2차 시도

## 영향력 평가를 위한 X, Y, Z의 왜도, 첨도, RMS 비교

~~~R
> summary(Nor)
     X_skew              X_kurt          X_rms             Y_skew             Y_kurt     
 Min.   :-0.388514   Min.   :1.484   Min.   :0.06325   Min.   :-1.33590   Min.   :1.633  
 1st Qu.:-0.106948   1st Qu.:1.639   1st Qu.:0.12769   1st Qu.:-0.65362   1st Qu.:1.971  
 Median :-0.004407   Median :1.740   Median :0.15515   Median :-0.37961   Median :2.491  
 Mean   :-0.007015   Mean   :1.763   Mean   :0.15583   Mean   :-0.31562   Mean   :2.676  
 3rd Qu.: 0.103469   3rd Qu.:1.851   3rd Qu.:0.18626   3rd Qu.:-0.07178   3rd Qu.:3.234  
 Max.   : 0.337307   Max.   :2.585   Max.   :0.25672   Max.   : 0.70563   Max.   :5.730  
     Y_rms            Z_skew            Z_kurt          Z_rms        
 Min.   :0.0834   Min.   :-0.5585   Min.   :1.984   Min.   :0.09762  
 1st Qu.:0.1176   1st Qu.: 0.1005   1st Qu.:2.773   1st Qu.:0.13080  
 Median :0.1576   Median : 0.2926   Median :3.085   Median :0.14427  
 Mean   :0.1817   Mean   : 0.2948   Mean   :3.238   Mean   :0.14878  
 3rd Qu.:0.2311   3rd Qu.: 0.5040   3rd Qu.:3.611   3rd Qu.:0.17116  
 Max.   :0.3584   Max.   : 1.1581   Max.   :6.322   Max.   :0.19521  
> summary(Wea)
     X_skew             X_kurt          X_rms             Y_skew             Y_kurt     
 Min.   :-0.70128   Min.   :1.704   Min.   :0.06076   Min.   :-0.42069   Min.   :1.564  
 1st Qu.:-0.29198   1st Qu.:2.081   1st Qu.:0.08938   1st Qu.:-0.01184   1st Qu.:1.924  
 Median :-0.14639   Median :2.232   Median :0.10146   Median : 0.15417   Median :2.088  
 Mean   :-0.13658   Mean   :2.238   Mean   :0.10358   Mean   : 0.13628   Mean   :2.107  
 3rd Qu.:-0.01865   3rd Qu.:2.388   3rd Qu.:0.11554   3rd Qu.: 0.26939   3rd Qu.:2.276  
 Max.   : 0.58035   Max.   :3.027   Max.   :0.15634   Max.   : 0.69593   Max.   :3.257  
     Y_rms             Z_skew             Z_kurt          Z_rms        
 Min.   :0.08087   Min.   :-0.44130   Min.   :1.805   Min.   :0.07924  
 1st Qu.:0.14144   1st Qu.: 0.06824   1st Qu.:2.642   1st Qu.:0.11069  
 Median :0.16300   Median : 0.24682   Median :2.969   Median :0.12303  
 Mean   :0.17232   Mean   : 0.23950   Mean   :3.054   Mean   :0.12478  
 3rd Qu.:0.19660   3rd Qu.: 0.40182   3rd Qu.:3.341   3rd Qu.:0.13547  
 Max.   :0.32191   Max.   : 1.62298   Max.   :8.966   Max.   :0.17846  
> mean(Nor$X_kurt)-mean(Wea$X_kurt)
[1] -0.4750472
> sd(Nor$X_kurt)-sd(Wea$X_kurt)
[1] -0.07844096
> 
> mean(Nor$X_skew)-mean(Wea$X_skew)
[1] 0.1295684
> sd(Nor$X_skew)-sd(Wea$X_skew)
[1] -0.08276183
> 
> mean(Nor$X_rms)-mean(Wea$X_rms)
[1] 0.05225036
> sd(Nor$X_rms)-sd(Wea$X_rms)
[1] 0.01881739
> 
> 
> 
> mean(Nor$Y_kurt)-mean(Wea$Y_kurt)
[1] 0.5692035
> sd(Nor$Y_kurt)-sd(Wea$Y_kurt)
[1] 0.5086896
> 
> mean(Nor$Y_skew)-mean(Wea$Y_skew)
[1] -0.4519043
> sd(Nor$Y_skew)-sd(Wea$Y_skew)
[1] 0.2471289
> 
> mean(Nor$Y_rms)-mean(Wea$Y_rms)
[1] 0.009393498
> sd(Nor$Y_rms)-sd(Wea$Y_rms)
[1] 0.02553229
> 
> 
> 
> mean(Nor$Z_kurt)-mean(Wea$Z_kurt)
[1] 0.1841672
> sd(Nor$Z_kurt)-sd(Wea$Z_kurt)
[1] 0.02519595
> 
> mean(Nor$Z_skew)-mean(Wea$Z_skew)
[1] 0.0553219
> sd(Nor$Z_skew)-sd(Wea$Z_skew)
[1] 0.04742077
> 
> mean(Nor$Z_rms)-mean(Wea$Z_rms)
[1] 0.02399614
> sd(Nor$Z_rms)-sd(Wea$Z_rms)
[1] 0.003565186
~~~

## New Checkfunction

~~~Matlab
function result=Checkfunction(data,func,filename)
    for k=1:height(data);
        if k>height(data)/2
            z={'Wear'};
        else k<=height(data)/2
            z={'Normal'};
        end
        p=func.predictFcn(data(k,:));
        Predict(k)=p;
        Result(k)=z;
    end
    
    Predict=Predict';
    Result=Result';
    
    result=table(Predict,Result);
    
    cd /Users/zerohertz/Downloads
    writetable(result,filename,'Delimiter',',')
    cd /Users/zerohertz/Documents/MATLAB/ML
end
~~~