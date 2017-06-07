---
title: Canny算子边缘检测
tags:
  - Canny算子
  - 边缘检测
id: 28
categories:
  - Programming
date: 2007-11-17 12:02:25
---

Canny认为一个优良的边缘检测算子应具有以下3个特性:

① 好的检测性能。不漏检真实边缘，也不把非边缘点作为边缘点检出，使输出的信噪比最大。

② 好的定位性能。检测到的边缘点与实际边缘点位置最近。

③ 唯一性。对于单个边缘点仅有一个响应。

<!--more-->

根据以上3个准则，Canny推导出最优边缘检测算子的一个近似实现是：边界点位于图像被高斯函数平滑后的梯度幅度的极大值点。

具体步骤:

1.首先利用一维高斯函数对图像进行平滑处理;

2.求的各点的梯度值;

3.非最大值抑制;

4.利用双门限跟踪轮廓.

传统的canny算法存在许多不足:

1.传统Canny算子在2×2邻域内求有限差均值来计算梯度幅值的算法，对噪声较敏感，且容易检测出假边缘或丢失一些真实边缘的细节部分.

提出了改进方法:采用在3×3邻域计算梯度幅值

2.传统的canny算子不能够实现自适应,很难实现自动化.根据相关论文,可以利用灰度共生矩阵的惯性矩特性得到一阶高斯差分和阀值.