---
title: >-
  Diagnosis Systems for Ball Bearing Cage Defects using Fisher Discriminant
  Ratio
date: 2020-07-29 11:51:10
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
mathjax: true
---
# Abstract

![Abstract](https://user-images.githubusercontent.com/42334717/90792834-f1f78300-e345-11ea-9563-22bd2a9604f4.png)

<!-- More -->

***

# Poster

![PP05-042 오효근](https://user-images.githubusercontent.com/42334717/91074437-811ed680-e677-11ea-8728-9699ddb3e62e.jpg)

[PP05-042 오효근.pdf](https://github.com/Zerohertz/zerohertz.github.io/files/5119228/PP05-042.pdf)

***

# Source

~~~R fdr.R
setwd("C:/Users/ohg34/Downloads")

normal=read.csv('normal.csv',header=F)
fault=read.csv('fault.csv',header=F)

normal=normal[100000:200000,1:4]
fault=fault[100000:200000,1:4]

fdr=function(data1,data2){
  ff=(mean(data1)-mean(data2))^2/((sd(data1))^2+(sd(data2))^2)
  return(ff)
}

allfdr=function(data1,data2){
  i=1
  while(i<=ncol(data1)){
    cat(i,' : ',fdr(data1[,i],data2[,i]),'\n')
    i=i+1
  }
}

sk=function(x,Winsiz){
  i=0
  sk=0
  while((i+Winsiz)<=length(x)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i+j]
      j=j+1
    }
    sk[i+1]<-sum(((sam-mean(sam))^3)/sd(sam)^3)*(1/(Winsiz-1))
    i=i+1
  }
  return(sk)
}

ku=function(x,Winsiz){
  i=0
  ku=0
  while((i+Winsiz)<=length(x)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i+j]
      j=j+1
    }
    ku[i+1]<-sum(((sam-mean(sam))^4)/sd(sam)^4)*(1/(Winsiz-1))
    i=i+1
  }
  return(ku)
}

rm=function(x,Winsiz){
  i=0
  rm=0
  while((i+Winsiz)<=length(x)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i+j]
      j=j+1
    }
    rm[i+1]<-sqrt(sum(sam^2)/Winsiz)
    i=i+1
  }
  return(rm)
}

p2p=function(x,Winsiz){
  i=0
  pp=0
  while((i+Winsiz)<=length(x)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i+j]
      j=j+1
    }
    pp[i+1]<-max(sam)-min(sam)
    i=i+1
  }
  return(pp)
}

iq=function(x,Winsiz){
  i=0
  qq=0
  while((i+Winsiz)<=length(x)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i+j]
      j=j+1
    }
    qq[i+1]<-IQR(sam)
    i=i+1
  }
  return(qq)
}

cf=function(x,Winsiz){
  i=0
  cc=0
  while((i+Winsiz)<=length(x)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i+j]
      j=j+1
    }
    cc[i+1]<-(max(sam)-min(sam))/(sqrt(sum(sam^2)/Winsiz))
    i=i+1
  }
  return(cc)
}

test=function(data,Winsiz){
  X_skew=sk(data$V2,Winsiz)
  X_kurt=ku(data$V2,Winsiz)
  X_rms=rm(data$V2,Winsiz)
  X_p2p=p2p(data$V2,Winsiz)
  X_iq=iq(data$V2,Winsiz)
  X_cf=cf(data$V2,Winsiz)
  Y_skew=sk(data$V3,Winsiz)
  Y_kurt=ku(data$V3,Winsiz)
  Y_rms=rm(data$V3,Winsiz)
  Y_p2p=p2p(data$V3,Winsiz)
  Y_iq=iq(data$V3,Winsiz)
  Y_cf=cf(data$V3,Winsiz)
  Z_skew=sk(data$V4,Winsiz)
  Z_kurt=ku(data$V4,Winsiz)
  Z_rms=rm(data$V4,Winsiz)
  Z_p2p=p2p(data$V4,Winsiz)
  Z_iq=iq(data$V4,Winsiz)
  Z_cf=cf(data$V4,Winsiz)
  all=cbind(X_skew,X_kurt,X_rms,X_p2p,X_iq,X_cf,Y_skew,Y_kurt,Y_rms,Y_p2p,Y_iq,Y_cf,Z_skew,Z_kurt,Z_rms,Z_p2p,Z_iq,Z_cf)
  options(max.print=10000000)
  return(all)
}

FDRtest=function(max,size,start){
  j=start
  i=1
  
  x_sk=0
  x_ku=0
  x_rm=0
  x_p2p=0
  x_iq=0
  x_cf=0
  y_sk=0
  y_ku=0
  y_rm=0
  y_p2p=0
  y_iq=0
  y_cf=0
  z_sk=0
  z_ku=0
  z_rm=0
  z_p2p=0
  z_iq=0
  z_cf=0
  
  while(j<=max){
    h=test(normal,j)
    f=test(fault,j)
    
    x_sk[i]<-fdr(f[,1],h[,1])
    x_ku[i]<-fdr(f[,2],h[,2])
    x_rm[i]<-fdr(f[,3],h[,3])
    x_p2p[i]<-fdr(f[,4],h[,4])
    x_iq[i]<-fdr(f[,5],h[,5])
    x_cf[i]<-fdr(f[,6],h[,6])
    y_sk[i]<-fdr(f[,7],h[,7])
    y_ku[i]<-fdr(f[,8],h[,8])
    y_rm[i]<-fdr(f[,9],h[,9])
    y_p2p[i]<-fdr(f[,10],h[,10])
    y_iq[i]<-fdr(f[,11],h[,11])
    y_cf[i]<-fdr(f[,12],h[,12])
    z_sk[i]<-fdr(f[,13],h[,13])
    z_ku[i]<-fdr(f[,14],h[,14])
    z_rm[i]<-fdr(f[,15],h[,15])
    z_p2p[i]<-fdr(f[,16],h[,16])
    z_iq[i]<-fdr(f[,17],h[,17])
    z_cf[i]<-fdr(f[,18],h[,18])
    
    print(j)
    
    if(i%%2==1){
      cat((j-start)/(max-start)*100,'%\n')
    }
    
    j=j+size
    i=i+1
  }
  data=cbind(x_sk,x_ku,x_rm,x_p2p,x_iq,x_cf,y_sk,y_ku,y_rm,y_p2p,y_iq,y_cf,z_sk,z_ku,z_rm,z_p2p,z_iq,z_cf)
  return(data)
}

fdr_dat=FDRtest(100000,10,10)
write.table(fdr_dat,'fdr.csv',sep=',',row.names=F)
~~~

~~~R Fast_fdr.R
setwd("C:/Users/ohg34/Downloads")

normal=read.csv('normal.csv',header=F)
fault=read.csv('fault.csv',header=F)

normal=normal[100000:2000000,1:4]
fault=fault[100000:2000000,1:4]

fdr=function(data1,data2){
  ff=(mean(data1)-mean(data2))^2/((sd(data1))^2+(sd(data2))^2)
  return(ff)
}

allfdr=function(data1,data2){
  i=1
  while(i<=ncol(data1)){
    cat(i,' : ',fdr(data1[,i],data2[,i]),'\n')
    i=i+1
  }
}


sk=function(x,Winsiz){
  i=0
  sk=0
  while(i<floor(length(x)/Winsiz)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i*Winsiz+j]
      j=j+1
    }
    sk[i+1]<-sum(((sam-mean(sam))^3)/sd(sam)^3)*(1/(Winsiz-1))
    i=i+1
  }
  return(sk)
}

ku=function(x,Winsiz){
  i=0
  ku=0
  while(i<floor(length(x)/Winsiz)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i*Winsiz+j]
      j=j+1
    }
    ku[i+1]<-sum(((sam-mean(sam))^4)/sd(sam)^4)*(1/(Winsiz-1))
    i=i+1
  }
  return(ku)
}

rm=function(x,Winsiz){
  i=0
  rm=0
  while(i<floor(length(x)/Winsiz)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i*Winsiz+j]
      j=j+1
    }
    rm[i+1]<-sqrt(sum(sam^2)/Winsiz)
    i=i+1
  }
  return(rm)
}

p2p=function(x,Winsiz){
  i=0
  pp=0
  while(i<floor(length(x)/Winsiz)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i*Winsiz+j]
      j=j+1
    }
    pp[i+1]<-max(sam)-min(sam)
    i=i+1
  }
  return(pp)
}

iq=function(x,Winsiz){
  i=0
  qq=0
  while(i<floor(length(x)/Winsiz)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i*Winsiz+j]
      j=j+1
    }
    qq[i+1]<-IQR(sam)
    i=i+1
  }
  return(qq)
}

cf=function(x,Winsiz){
  i=0
  cc=0
  while(i<floor(length(x)/Winsiz)){
    j=1
    sam=0
    while(j<=Winsiz){
      sam[j]=x[i*Winsiz+j]
      j=j+1
    }
    cc[i+1]<-(max(sam)-min(sam))/(sqrt(sum(sam^2)/Winsiz))
    i=i+1
  }
  return(cc)
}

test=function(data,Winsiz){
  X_skew=sk(data$V2,Winsiz)
  X_kurt=ku(data$V2,Winsiz)
  X_rms=rm(data$V2,Winsiz)
  X_p2p=p2p(data$V2,Winsiz)
  X_iq=iq(data$V2,Winsiz)
  X_cf=cf(data$V2,Winsiz)
  all=cbind(X_skew,X_kurt,X_rms,X_p2p,X_iq,X_cf)
  options(max.print=10000000)
  return(all)
}

FDRtest=function(max,size,start){
  j=start
  i=1
  
  x_sk=0
  x_ku=0
  x_rm=0
  x_p2p=0
  x_iq=0
  x_cf=0
  
  while(j<=max){
    h=test(normal,j)
    f=test(fault,j)
    
    x_sk[i]<-fdr(f[,1],h[,1])
    x_ku[i]<-fdr(f[,2],h[,2])
    x_rm[i]<-fdr(f[,3],h[,3])
    x_p2p[i]<-fdr(f[,4],h[,4])
    x_iq[i]<-fdr(f[,5],h[,5])
    x_cf[i]<-fdr(f[,6],h[,6])
    
    print(j)
    
    if(i%%2==1){
      cat((j-start)/(max-start)*100,'%\n')
    }
    
    j=j+size
    i=i+1
  }
  data=cbind(x_sk,x_ku,x_rm,x_p2p,x_iq,x_cf)
  return(data)
}

fdr_dat=FDRtest(100000,1000,1000)
write.table(fdr_dat,'fdr.csv',sep=',',row.names=F)
~~~