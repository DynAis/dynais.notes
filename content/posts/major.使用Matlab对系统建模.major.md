---
title: "使用Matlab对系统建模"
# author: 
tags:
  - Matlab
  - 信号与系统
date: '2022-04-17'
ShowToc: true
draft: false
---
介绍了Matlab中对系统建模常用的一些方法
<!--more-->

---
- 信号与系统
- Matlab

## 1 库函数
![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/202204170020665.png?x-oss-process=image/format,jpg/interlace,1#center)

## 2 Templet

```matlab
clc;
clear all;
close all;

%% Initialisierung der Ubertragungsfunktionen
T1 = 1;             % Zeitkonstante T1 in s
T2 = 0.1;           % Zeitkonstante T2 in s

Z1 = [T1 0];        % Zahler von G1(s)
N1 = [T1 1];        % Nenner von G1(s)

Z2 = [1];           % Zahler von G2(s)
N2 = [T2 1];        % Nenner von G2(s)

G1 = tf(Z1,N1);     % Ubertragungsfunktion G1 aus Z1 und N1
G2 = tf(Z2,N2);     % Ubertragungsfunktion G2 aus Z2 und N2
G3 = G1*G2;         % Hintereinanderschaltung von G1 und G2 zu G3

%% Darstellung von Sprung- und Impulsantworten
figure(1)
step(G1);
hold on;
step(G2);
legend('Hochpass','Tiefpass');
title('Sprungantworten');

figure(2)
impulse(G1);
hold on;
impulse(G2);
legend('Hochpass','Tiefpass');
title('Impulsantworten');

%% Darstellung von Pol-Nullstellen-Plan 
figure(3)
pzmap(G1);
hold on;
pzmap(G2);
legend('Hochpass','Tiefpass');
title('Pol-Nullstellen-Diagramm');

%% Darstellung der Ortskurve 
figure(4)
h = nyquistplot(G1);
setoptions(h,'ShowFullContour','off');      % Eliminieren von negativen Frequenzen
hold on;
h2 = nyquistplot(G2);
setoptions(h2,'ShowFullContour','off');     % Eliminieren von negativen Frequenzen
legend('Hochpass','Tiefpass');
title('Ortskurven');

%% Darstellung der Bode-Diagramme 
figure(5)
bode(G1);
hold on;
bode(G2);
bode(G3);
legend('Hochpass','Tiefpass','Bandpass');
title('Bode-Diagramme');
```

## 参考