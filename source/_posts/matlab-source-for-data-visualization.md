---
title: Matlab source for data visualization
date: 2020-03-18 12:15:52
categories:
- Matlab
tags:
- Matlab
- PHM
- Statistics
mathjax: true
---
# Slicing

~~~Matlab
write(fault1(300001:1800000,:),'fault1.csv','Delimiter',',')
~~~

***

# 기본 Plot

~~~Matlab
a=plot(fault9.time,fault9.Y,'Color','red');
hold on
b=plot(normal5.time,normal5.Y,'Color','blue');
legend('fault','normal')
axis([180 1100 -10 10])
xlabel('Time(sec)')
ylabel('Acc of Y(m/s^2)')
title('Acc of Y')
set(gca,'fontsize',20)
a.Color(4)=0.5;
b.Color(4)=0.5;
~~~

+ `legend('name_1','name_2')`로 범례 삽입
+ `axis([X_min X_max Y_min Y_max])`로 스케일 조정 가능
+ `xlabel('name')`, `ylabel('name')`로 축의 이름 지정
+ `title('name')`로 plot의 이름 지정
+ `set(gca,'fontsize',20)`으로 폰트의 크기 지정
+ `plot.Color(4)`로 투명도 지정

<!-- More -->

***

# Histogram

~~~Matlab
histogram(fault6.X,'BinWidth',0.1,'Normalization','probability','FaceColor','red')
hold on
histogram(fault7.X,'BinWidth',0.1,'Normalization','probability','FaceColor','blue')
histogram(fault8.X,'BinWidth',0.1,'Normalization','probability','FaceColor','yellow')
histogram(fault9.X,'BinWidth',0.1,'Normalization','probability','FaceColor','green')
histogram(fault5.X,'BinWidth',0.1,'Normalization','probability','FaceColor','black')
~~~