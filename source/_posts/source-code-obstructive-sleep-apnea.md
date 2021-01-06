---
title: Source Code(Obstructive Sleep Apnea)
date: 2020-07-27 18:27:01
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
- Arduino
- C, C++
- RaspberryPi
- Python
- Sleep apnea
mathjax: true
---
# Prototype 1(Arduino, Computer)

## Arduino

~~~C++ Senosr.ino
void setup() {
  Serial.begin(2000000);
}

void loop() {
  int x_val = analogRead(A0);
  int y_val = analogRead(A1);
  int z_val = analogRead(A2);

  int AE = analogRead(A7);
  
  if(AE >= 500){
    AE = 1;
  }
  else{
    AE = 0;
  }
  
  Serial.print(x_val);
  Serial.print(",");
  Serial.print(y_val);
  Serial.print(",");
  Serial.print(z_val);
  Serial.print(",");
  Serial.print(AE);
  Serial.print("\n");

  delay(20);
}
~~~

<!-- More -->

## C++

~~~C++ Serial.cpp
#include <iostream>
#include <string>
#include <cstring>
#include "CSerialComm.h"
#include <chrono>
#include <fstream>
#include <windows.h>
#pragma warning(disable:4996)

using namespace std;

int main()
{
	CSerialComm SerialComm;

	ofstream file;
	cout << "File name : ";
	string nameOfFile;
	cin >> nameOfFile;
	nameOfFile = nameOfFile + ".csv";
	file.open(nameOfFile);
	cout << "Port num : ";
	string port_name;
	cin >> port_name;
	char port[10];
	strcpy(port, port_name.c_str());

	if (SerialComm.connect(port))
		printf("Serial port is connected!!\n");
	else
		printf("Sercial connection fail!!\n");

	Sleep(1000);

	int i = 0;
	BYTE data_init[32];
	int j = 0;

	while (j < 10) {
		i = 0;
		while (1) {
			SerialComm.readCommand(data_init[i]);
			if (data_init[i] == '\n') {
				j++;
				break;
			}
			i++;
			cout << j << endl;
		}
	}
	BYTE data[32];

	i = 0;
	chrono::system_clock::time_point start = std::chrono::system_clock::now();
	chrono::duration<double> sec = std::chrono::system_clock::now() - start;
	while (1)
	{
		if (GetAsyncKeyState(VK_ESCAPE)) break;
		sec = std::chrono::system_clock::now() - start;
		i = 0;
		while (1) {
			SerialComm.readCommand(data[i]);
			if (data[i] == '\n'){
				string time = to_string(sec.count());
				string str_data(data, data + i + 1);
				string str = time + ',' + str_data;
				cout << str;
				file << str;
				break;
			}
			i++;
		}
	}
	file.close();
	return 0;
}
~~~

~~~C++ CSerialComm.h
#include "serialport.h"

#define RETURN_SUCCESS 1
#define RETURN_FAIL 0


class CSerialComm
{
public:
	CSerialComm();
	~CSerialComm();

	CSerialPort	serial;
	int		connect(char* _portNum);
	int		readCommand(BYTE &p);
	void		disconnect();
};
~~~

~~~C++ CSerialComm.cpp
#include "CSerialComm.h"


CSerialComm::CSerialComm() {}
CSerialComm::~CSerialComm() {}


int CSerialComm::connect(char* portNum)
{
	if (!serial.OpenPort(portNum))
		return RETURN_FAIL;

	serial.ConfigurePort(2000000, 8, FALSE, NOPARITY, ONESTOPBIT);
	serial.SetCommunicationTimeouts(0, 0, 0, 0, 0);

	return RETURN_SUCCESS;
}


int CSerialComm::readCommand(BYTE &p)
{
	if (serial.ReadByte(p))
		return RETURN_SUCCESS;
	else
		return RETURN_FAIL;
}

void CSerialComm::disconnect()
{
	serial.ClosePort();
}
~~~

***

# Prototype 2(Arduino nano 33 BLE, RaspberryPi)

## Arduino

~~~C++ peripheral.ino
#include <ArduinoBLE.h>
#include <Arduino_LSM9DS1.h>

BLEService ACC("1001");
BLEFloatCharacteristic accX("2001", BLERead | BLENotify);
BLEFloatCharacteristic accY("2002", BLERead | BLENotify);
BLEFloatCharacteristic accZ("2003", BLERead | BLENotify);

BLEService GYRO("1002");
BLEFloatCharacteristic gyroX("2011", BLERead | BLENotify);
BLEFloatCharacteristic gyroY("2012", BLERead | BLENotify);
BLEFloatCharacteristic gyroZ("2013", BLERead | BLENotify);

BLEService MAG("1003");
BLEFloatCharacteristic magX("2021", BLERead | BLENotify);
BLEFloatCharacteristic magY("2022", BLERead | BLENotify);
BLEFloatCharacteristic magZ("2023", BLERead | BLENotify);

float acc_x, acc_y, acc_z;
float gyro_x, gyro_y, gyro_z;
float mag_x, mag_y, mag_z;

void setup() {
  Serial.begin(115200);
  
  if(!BLE.begin()) {
    Serial.println("Starting BLE Failed!");
    while(1);
  }

  if (!IMU.begin()) { //LSM9DSI센서 시작
    Serial.println("LSM9DSI센서 오류!");
    while (1);
  }
  
  BLE.setDeviceName("IMU");
  BLE.setLocalName("IMU");
  
  BLE.setAdvertisedService(ACC);
  BLE.setAdvertisedService(GYRO);
  BLE.setAdvertisedService(MAG);
  ACC.addCharacteristic(accX);
  ACC.addCharacteristic(accY);
  ACC.addCharacteristic(accZ);
  GYRO.addCharacteristic(gyroX);
  GYRO.addCharacteristic(gyroY);
  GYRO.addCharacteristic(gyroZ);
  MAG.addCharacteristic(magX);
  MAG.addCharacteristic(magY);
  MAG.addCharacteristic(magZ);
  BLE.addService(ACC);
  BLE.addService(GYRO);
  BLE.addService(MAG);
  BLE.setConnectable(true);
  BLE.setAdvertisingInterval(100);
  BLE.advertise();
  Serial.println("Bluetooth Device Active, Waiting for Connections...");
}

void loop() {
  BLEDevice central = BLE.central();

  if(central) {
    Serial.print("Connected to Central: ");
    Serial.println(central.address());
    while(central.connected()) {
      IMU.readAcceleration(acc_x, acc_y, acc_z);
      IMU.readGyroscope(gyro_x, gyro_y, gyro_z);
      IMU.readMagneticField(mag_x, mag_y, mag_z);      
      accX.writeValue(acc_x);
      accY.writeValue(acc_y);
      accZ.writeValue(acc_z);
      gyroX.writeValue(gyro_x);
      gyroY.writeValue(gyro_y);
      gyroZ.writeValue(gyro_z);
      magX.writeValue(mag_x);
      magY.writeValue(mag_y);
      magZ.writeValue(mag_z);
      Serial.println(acc_x);
    }
  }
  Serial.print("Disconnected from Central: ");
  Serial.println(BLE.address());
}
~~~

~~~C++ central.ino
#include <ArduinoBLE.h>

union dat{
  unsigned char asdf[4];
  float zxcv;
};

float getData(const unsigned char data[], int length) {
  dat dat;
  for (int i = 0; i < length; i++) {
    dat.asdf[i] = data[i]; 
    }
  return dat.zxcv;
}

void printcsv(BLECharacteristic c1, BLECharacteristic c2, BLECharacteristic c3, BLECharacteristic c4, BLECharacteristic c5, BLECharacteristic c6, BLECharacteristic c7, BLECharacteristic c8, BLECharacteristic c9){
  c1.read();
  c2.read();
  c3.read();
  c4.read();
  c5.read();
  c6.read();
  c7.read();
  c8.read();
  c9.read(); 
  float f1=getData(c1.value(), c1.valueLength());
  float f2=getData(c2.value(), c2.valueLength());
  float f3=getData(c3.value(), c3.valueLength());
  float f4=getData(c4.value(), c4.valueLength());
  float f5=getData(c5.value(), c5.valueLength());
  float f6=getData(c6.value(), c6.valueLength());
  float f7=getData(c7.value(), c7.valueLength());
  float f8=getData(c8.value(), c8.valueLength());
  float f9=getData(c9.value(), c9.valueLength());
  Serial.print(f1);
  Serial.print(',');
  Serial.print(f2);
  Serial.print(',');
  Serial.print(f3);
  Serial.print(',');
  Serial.print(f4);
  Serial.print(',');
  Serial.print(f5);
  Serial.print(',');
  Serial.print(f6);
  Serial.print(',');
  Serial.print(f7);
  Serial.print(',');
  Serial.print(f8);
  Serial.print(',');
  Serial.print(f9);
  Serial.print('\n');
}

void setup() {
  Serial.begin(115200);

  if(!BLE.begin()) {
    Serial.println("Starting BLE Failed!");
    while(1);
  }
  BLE.scan();
}

void loop() {
  BLEDevice peripheral = BLE.available();

  if(peripheral){
    if(peripheral.localName()=="IMU"){
      BLE.stopScan();
      if(peripheral.connect()){
        Serial.println("Connect1");
      }
      else{
        return;
      }
      if(peripheral.discoverAttributes()){
        Serial.println("Connect2");
      }
      else{
        return;
      }
      BLEService acc=peripheral.service("1001");
      BLECharacteristic accx=acc.characteristic("2001");
      BLECharacteristic accy=acc.characteristic("2002");
      BLECharacteristic accz=acc.characteristic("2003");
      BLEService gyro=peripheral.service("1002");
      BLECharacteristic gyrox=gyro.characteristic("2011");
      BLECharacteristic gyroy=gyro.characteristic("2012");
      BLECharacteristic gyroz=gyro.characteristic("2013");
      BLEService mag=peripheral.service("1003");
      BLECharacteristic magx=mag.characteristic("2021");
      BLECharacteristic magy=mag.characteristic("2022");
      BLECharacteristic magz=mag.characteristic("2023");
      while(true){
//        accx.read();
//        float f1=getData(accx.value(),accx.valueLength());
//        Serial.print(f1);
//        Serial.print(',');
//        accy.read();
//        float f2=getData(accy.value(),accy.valueLength());
//        Serial.print(f2);
//        Serial.print(',');
//        accz.read();
//        float f3=getData(accz.value(),accz.valueLength());
//        Serial.println(f3);
        if(peripheral.connected()){
          printcsv(accx,accy,accz,gyrox,gyroy,gyroz,magx,magy,magz);
        }
        else{
          peripheral.disconnect();
          return;
        }
      }
    }
  }
  BLE.scan();
  Serial.println("rescan");
}
~~~

## Python

~~~Python ser.py
import serial
import time

ser = serial.Serial('/dev/ttyACM0', 115200)
f = open('filename.csv', 'w', encoding = 'utf-8')
t = time.time()

try:
    while True:
        if ser.in_waiting != 0:
            t1 = time.time() - t
            t2 = round(t1, 5)
            t3 = str(t2)
            sensor = ser.readline()
            print(t3)
            print(sensor.decode())
            f.write(t3)
            f.write(',')
            f.write(sensor.decode())
except:
    f.close()
~~~

***

# R

## Undersampling

~~~R undersampling.R
setwd("/Users/zerohertz/MATLAB/Obstructive Sleep Apnea/")

del=read.csv("delta.csv",header=T)

del0=subset(del,subset=(del$Sleep==0))
del10=subset(del,subset=(del$Sleep==10))
del20=subset(del,subset=(del$Sleep==20))
del30=subset(del,subset=(del$Sleep==30))
del40=subset(del,subset=(del$Sleep==40))

s1=del10[sample(nrow(del10),1252,replace=FALSE),]
s2=del20[sample(nrow(del20),10954,replace=FALSE),]
s3=del30[sample(nrow(del30),1643,replace=FALSE),]
s4=del40[sample(nrow(del40),4421,replace=FALSE),]

sleep=rbind(s1,s2,s3,s4)

write.table(sleep,file="sl1.csv",sep=",",row.names=F,col.names=T)
~~~

## Make Label Data

~~~R MakeLabelData
i = 1

while(i <= length(raw[,1])){
	time=raw[i,1]
	ti=time%/%30+1
	raw[i,6]=lab[ti,1]
  if(lab[ti,1]=='W'){
    raw[i,7]=0
  }
  else if(lab[ti,1]=='N1'){
    raw[i,7]=10
  }
  else if(lab[ti,1]=='N2'){
    raw[i,7]=20
  }
  else if(lab[ti,1]=='N3'){
    raw[i,7]=30
  }
	else if(lab[ti,1]=='R'){
    raw[i,7]=40
  }
  i=i+1
}
write.table(raw,file="label.csv",sep=",",row.names=F,col.names=F)
~~~

***

# DNF Number

~~~Matlab dnf.m
function dnf_num = dnf(c1, c2, al, be)
    dnf_num = 1/(al+be)*(al*(kurtosis(c1)/kurtosis(c2))+be*(sqrt(var(c1))/sqrt(var(c2))));
end
~~~

***

# HRV(Heart Rate Variability)

## Detecting R-R Interval

~~~Matlab rrInterval.mat
function [qrspeaks, locs, y] = rrInterval(time, ecg)
t = time;
wt = modwt(ecg, 5);
wtrec = zeros(size(wt));
wtrec(4:5, :) = wt(4:5, :);
y = imodwt(wtrec, 'sym4');
y = abs(y).^2;
[qrspeaks, locs] = findpeaks(y, t, 'MinPeakHeight', 0.15, 'MinPeakDistance', 0.450); %time과 y에 대한 그래프를 해석 후 파라미터 결정
end
~~~

> ECG

<img width="672" alt="ECG" src="https://user-images.githubusercontent.com/42334717/103261452-fbc07f80-49e4-11eb-8181-4251df1a5af5.png">

~~~Matlab
>> load mit200
>> plot(tm, ecgsig)
~~~

> R Peaks Localized by Wavelet Transform with Automatic Annotations

<img width="1051" alt="R Peaks Localized by Wavelet Transform with Automatic Annotations" src="https://user-images.githubusercontent.com/42334717/103263042-11847380-49ea-11eb-8daa-b840f7f837a5.png">

~~~Matlab
>> [qr, lo, y] = rrInterval(tm, ecgsig);
>> plot(tm, y)
>> hold on
>> plot(lo, qr, 'ro')
>> plot(tm(ann), y(ann), 'k*')
>> grid on
~~~

## Make HRV Data from R-R Interval

~~~Matlab makeHRV.m
function [time, val] = makeHRV(locat)
for num = (1:length(locat)-1)
    val(num) = locat(num + 1) - locat(num);
    time(num) = locat(num);
end
end
~~~

> HRV

![HRV](https://user-images.githubusercontent.com/42334717/103266138-4f859580-49f2-11eb-8ca9-ee74b18e45d7.jpg)

~~~Matlab checkRR.m
function [] = checkRR(paramName, size, param)
cd apnea-ecg-database-1.0.0/
wfdb2mat(paramName);
[tm, data] = rdmat(append(paramName, 'm'));
cd ..

ecg = data(:, 1);
tm = tm(1:(length(tm)/10));
ecg = ecg(1:(length(ecg)/10));
ra = fix(rand() * length(tm) / 200);

[qr, lo, y] = rrIntervalparam(tm, ecg, param);
[tt, hh] = makeHRV(lo);

i = 1;

for N = lo
    num = find(tm == N);
    rPeak(i) = ecg(num);
    i = i + 1;
end

fig = figure;
set(fig, 'Position', [0 0 1920 1080])

subplot(3,1,1)
plot(tm, ecg, 'LineWidth', 1)
hold on
plot(lo, rPeak, 'ro')
axis([ra ra + size -1 3])
xlabel('Time(sec)')
ylabel('ECG(mV)')
grid on
set(gca, 'fontsize', 15)

subplot(3,1,2)
plot(tm, y, 'LineWidth', 1)
hold on
plot(lo, qr, 'ro')
axis([ra ra + size 0 0.9])
xlabel('Time(sec)')
ylabel('Amplitude')
grid on
set(gca, 'fontsize', 15)

subplot(3,1,3)
bar(tt, hh, 0.01)
hold on
plot(tt, hh, 'ro')
axis([ra ra + size 0 2])
xlabel('Time(sec)')
ylabel('HRV(sec)')
grid on
set(gca, 'fontsize', 15)

cd RR/
saveas(gca, append(append(paramName, 'checkRR', string(param)), '.bmp'))
cd ..
end
~~~

***

# Condition Indicators of HRV

> Data 사용

~~~Matlab
wfdb2mat('FileName');
[tm, ecg, Fs, labels] = rdmat('FileName' + 'm');
[apn_tm, apn]= rdann('FileName', 'apn');
~~~

## Time Domain Analysis



## Frequency Domain Analysis

~~~Matlab freqHRV.m
function [f, P1] = freqHRV(hrv, Length, SamplingTime)
y=fft(hrv);
SamplingRate = Length / SamplingTime;
P2 = abs(y/Length);
P1 = P2(1:fix(Length/2)+1);
P1(2:end-1) = 2*P1(2:end-1);
f = SamplingRate * (0:(Length/2))/Length;
end
~~~

~~~Matlab freqHRV1.m
function [f, P1] = freqHRV1(hrv, Length, SamplingTime)
SamplingRate = Length / SamplingTime;
NFFT = 2^(ceil(log2(length(hrv))));
Y = fft(hrv, NFFT) / Length;
f = SamplingRate / 2 * linspace(0, 1, NFFT / 2 + 1);
P1 = 2*abs(Y(1:fix(NFFT/2+1)));
end
~~~

~~~Matlab freqHRVanalysis.m
function [VLF, LF, HF] = freqHRVanalysis(freq, amp)
i = 1;
j = 1;
k = 1;
VLF_amp(1) = 1;
LF_amp(1) = 1;
HF_amp(1) = 1;
for num = (1:length(freq))
    if 0.003 <= freq(num) && freq(num) < 0.05
        %VLF_freq(i) = freq(num);
        VLF_amp(i) = amp(num)^2;
        i = i + 1;
    elseif 0.05 <= freq(num) && freq(num) < 0.15
        %LF_freq(j) = freq(num);
        LF_amp(j) = amp(num)^2;
        j = j + 1;
    elseif 0.15 <= freq(num) && freq(num) <= 0.4
        %HF_freq(k) = freq(num);
        HF_amp(k) = amp(num)^2;
        k = k + 1;
    end      
end
VLF = mean(VLF_amp);
LF = mean(LF_amp);
HF = mean(HF_amp); 
end
~~~

~~~Matlab windowHRV.m
function [f, P] = windowHRV(time, ECG, SamplingRate, Winsize)
%Sampling Rate(Hz)
%Window size(Min)
SamplingTime = Winsize * 60;
Win = fix(SamplingRate * SamplingTime);
num = fix(length(ECG) / Win) - 10;

% [~,ll,~]=rrInterval(time, ECG);
% [~,bb]=makeHRV(ll);
% freqHRVplot1(bb, length(bb), length(bb) / 100);

for N = (1:num)
    Time_Arr(:, N) = time(Win * (N - 1) + 1:Win * N);
    ECG_Arr(:, N) = ECG(Win * (N - 1) + 1:Win * N);
end

f = NaN(1000, num);
P = NaN(1000, num);

for N = (1:num)
    [~, lo, ~] = rrInterval(Time_Arr(:, N), ECG_Arr(:, N));
    [~, HRV] = makeHRV(lo);
    [fr, P1] = freqHRV1(HRV, length(HRV), SamplingTime);
    f(1:length(fr), N) = fr;
    P(1:length(P1), N) = P1;
end
end
~~~

~~~Matlab windowSpO2.m
function [SpO2] = windowSpO2(data, SamplingRate, Winsize)
SamplingTime = Winsize * 60;
Win = fix(SamplingRate * SamplingTime);
num = fix(length(data) / Win) - 10;

for N = (1:num)
    SpO2_Arr(:, N) = data(Win * (N - 1) + 1:Win * N);
end

for N = (1:num)
    SpO2(N) = mean(SpO2_Arr(:, N));
end
end
~~~

~~~Matlab freqHRVCI.m
function [F] = freqHRVCI(f, P)
for N = (1:length(f(1,:)))
[f1, f2, f3] = freqHRVanalysis(f(:, N), P(:, N));
F(N, 1) = f1;
F(N, 2) = f2;
F(N, 3) = f3;
end
end
~~~

~~~Matlab makeTableofHRV.m
function [tab] = makeTableofHRV(tm, data, SamplingRate, Windowsize, Apn)
[f, p] = windowHRV(tm, data(:, 1), SamplingRate, Windowsize);
F = freqHRVCI(f, p);
sp = windowSpO2(data(:, 5), SamplingRate, Windowsize);

tab = table(F(:, 1), F(:, 2), F(:, 3), sp');
tab.Properties.VariableNames{'Var1'} = 'VLF';
tab.Properties.VariableNames{'Var2'} = 'LF';
tab.Properties.VariableNames{'Var3'} = 'HF';
tab.Properties.VariableNames{'Var4'} = 'SpO2';
end
~~~

~~~Matlab makeLabelofHRV.m
function [tab] = makeLabelofHRV(tm, ecg, SamplingRate, Windowsize, tmApn, Apn)
init = tmApn(1);
tm = tm(init:length(tm));
ecg = ecg(init:length(ecg));

[f, p] = windowHRV(tm, ecg, SamplingRate, Windowsize);
F = freqHRVCI(f, p);

for N = (1:length(F)) % 78(Normal) / 65(Apnea)
    apn(N) = mean(Apn(Windowsize * (N - 1) + 1:Windowsize * N));
end

apn = abs(apn - 78) / (78 - 65);
tab = table(F(:, 1), F(:, 2), F(:, 3), apn');
tab.Properties.VariableNames{'Var1'} = 'VLF';
tab.Properties.VariableNames{'Var2'} = 'LF';
tab.Properties.VariableNames{'Var3'} = 'HF';
tab.Properties.VariableNames{'Var4'} = 'apn';
end
~~~

~~~Matlab apneaFreqPlot.m
function [tab] = apneaFreqPlot(paramName, Winsize)
cd apnea-ecg-database-1.0.0/
wfdb2mat(paramName);
[tm, data] = rdmat(append(paramName, 'm'));
[tmApn, apn] = rdann(paramName, 'apn');
cd ..

tab = makeLabelofHRV(tm, data, 100, Winsize, tmApn, apn);

tim = (1:height(tab))*Winsize;


fig = figure;
set(fig, 'Position', [0 0 1920 1080])

subplot(3,1,1)
plot(tim, tab.HF, 'Color', 'black', 'LineWidth', 1.2)
hold on
plot(tim(tab.apn == 0), tab.HF(tab.apn == 0), 'Color', 'blue', 'Marker', 'o', 'LineWidth', 2, 'LineStyle', 'none')
plot(tim(tab.apn > 0), tab.HF(tab.apn > 0), 'Color', 'red', 'Marker', '*', 'LineWidth', 2, 'LineStyle', 'none')
legend('HF', 'Normal', 'Apnea')
xlabel('Time(min)')
ylabel('Amplitude')
grid on
set(gca, 'fontsize', 15)

subplot(3,1,2)
plot(tim, tab.LF, 'Color', 'black', 'LineWidth', 1.2)
hold on
plot(tim(tab.apn == 0), tab.LF(tab.apn == 0), 'Color', 'blue', 'Marker', 'o', 'LineWidth', 2, 'LineStyle', 'none')
plot(tim(tab.apn > 0), tab.LF(tab.apn > 0), 'Color', 'red', 'Marker', '*', 'LineWidth', 2, 'LineStyle', 'none')
legend('LF', 'Normal', 'Apnea')
xlabel('Time(min)')
ylabel('Amplitude')
grid on
set(gca, 'fontsize', 15)

subplot(3,1,3)
plot(tim, tab.VLF, 'Color', 'black', 'LineWidth', 1.2)
hold on
plot(tim(tab.apn == 0), tab.VLF(tab.apn == 0), 'Color', 'blue', 'Marker', 'o', 'LineWidth', 2, 'LineStyle', 'none')
plot(tim(tab.apn > 0), tab.VLF(tab.apn > 0), 'Color', 'red', 'Marker', '*', 'LineWidth', 2, 'LineStyle', 'none')
legend('VLF', 'Normal', 'Apnea')
xlabel('Time(min)')
ylabel('Amplitude')
grid on
set(gca, 'fontsize', 15)

cd plot/
saveas(gca, append(paramName, '.bmp'))
cd ..
end
~~~

> 1min

<img width="1590" alt="1min" src="https://user-images.githubusercontent.com/42334717/103643395-f4c2df80-4f97-11eb-9a15-2fd5a7b9a5e2.png">

> 5min

<img width="1590" alt="5min" src="https://user-images.githubusercontent.com/42334717/103643405-fa202a00-4f97-11eb-980f-1bb66f5a9e10.png">

~~~Matlab makeTrainData.m
function [tab] = makeTrainData(paramName, Winsize)
cd apnea-ecg-database-1.0.0/
wfdb2mat(paramName);
[tm, data] = rdmat(append(paramName, 'm'));
[tmApn, apn] = rdann(paramName, 'apn');
cd ..

tab = makeLabelofHRV(tm, data, 100, Winsize, tmApn, apn);

for N = 1:height(tab)
    if tab.apn(N) == 0
        tab.label(N) = "Normal";
    else
        tab.label(N) = "Apnea";
    end
end
end
~~~