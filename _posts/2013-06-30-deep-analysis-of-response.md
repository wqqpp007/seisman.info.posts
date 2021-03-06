---
title: 仪器响应实例分析
date: 2013-06-30
modified: 2014-06-10
author: SeisMan
categories: 地震学基础
tags: 仪器响应
mathjax: true
---

仪器响应水很深，用起来容易，弄明白每一个参数却不简单，幸好 SEED 的 manual 提供了一个例子，可以帮助
理解，不过其写得太复杂、毫无重点且有些地方打印有错误，故而这里整理并改写一下。

这个仪器响应依然是标准的三个阶段：地震仪（运动信号转电压信号）、离散器（模电转换器）、FIR
滤波器。

<!--more-->

## Stage 1

假定仪器的自然频率为 $f_0=1Hz$，阻尼常数为 $\lambda=0.7$，该仪器的加速度传递函数为

$$H(s) = \frac{s}{s^2+2\lambda \omega_0 s + \omega_0^2}$$

对于这样一个传递函数，需要注意如下几点：

1.  该传递函数仅表示某一类地震仪的传递函数，现代地震仪的传递函数可能比这个更复杂；
2.  根据该传递函数，很容易计算出它的一个零点和两个极点；
3.  该仪器在 $f_s=1 Hz$ 时的 Sensitivity 为 $S_d=150V/m\cdot s^{-2}$。即地震仪接收到的地面
    运动加速度，如果 1 Hz 时加速度为 $1 m/s^2$，则地震仪的输出电压为 150V。
4.  仪器真实的传递函数应该是 $G(f)=R(f)*S_d=A_0*H(s)*S_d$。其中 $A_0$ 为归一化因子，
    即保证在频率 $f=f_s$ 时有 $|R(f_s)|=1.0$。

## Stage 2

使用的模数转换器 ADC 为 24bit 的，即输出最大值可以为 $\pm 2^{23}$，如果 ADC 所能转换的电压范围
为 $\pm 20V$，则 ADC 的放大系数为 $S_d=\frac{2^{23}}{20}=4.1943*10^{5} counts/V$。
这样一个 ADC 在输入电压为 1V 的情况下，其输出为 $4.1943*10^{5}$counts。结合地震仪的放大系数，
$1 m/s^2$ 的地面运动加速度将导致输出为

$$1 m/s^2 * 150 \frac{V}{m/s^2} * 4.1943\times 10^5 \frac{counts}{V} = 6.29145*10^7 counts$$

另一方面，ADC 的输入电压上限为 20V，这似乎也限制了该仪器所能记录到的最大加速度为
$20/150=0.13 m/s^2$。

## Stage 3

这个阶段的 FIR 滤波器通过给定多项式系数来实现。给定系数之后即可计算其响应函数，并计算该响应
函数在 1 Hz 处的振幅，然后得到归一化因子即为该阶段的放大系数为 1.9938。

## Stage 0

最终得到的放大系数为

$$Sd= 150 \frac{V}{m/s^2} \cdot 4.1943\times 10^5 \frac{counts}{V} \cdot 1.9938 \frac{counts}{counts}$$
$$=1.25439\times 10^8 \frac{counts}{m/s^2}$$

最后不要忘了第一阶段的无单位的归一化因子 $A_0$。

## 参考

-   [SEED Reference Manual](http://www.fdsn.org/seed_manual/SEEDManual_V2.4.pdf), Version 2.4, August 2012, P162-169

## 修订历史

-   2013-06-30：初稿；
-   2014-06-10：修订关于自然频率和归一化频率的问题；Thanks to 张申健；
