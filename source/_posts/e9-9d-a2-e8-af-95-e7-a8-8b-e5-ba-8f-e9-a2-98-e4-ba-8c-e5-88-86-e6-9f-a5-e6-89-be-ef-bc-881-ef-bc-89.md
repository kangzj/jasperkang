---
title: 面试程序题-二分查找（1）
id: 1989
comment: false
categories:
  - Programming
date: 2014-04-09 10:02:11
tags:
---

一个数组，大小先减后增，请找到增减部分的分界点，要求算法时间复杂度O(logN)。

下面给出了一个递归实现的版本。

这个问题还可以让查找其中的某个元素，也是二分，思路一样。
> #include &lt;iostream&gt;
> #define MAX 13
> using namespace std;
> void findBreakpoint(int* a, int starti, int endi){
> int i = (endi-starti)/2+starti;
> if(starti==i){
> cout&lt;&lt;i&lt;&lt;endl;
> return;
> }
> if(a[i]&lt;a[i+1]){
> findBreakpoint(a, starti, i);
> }else{
> findBreakpoint(a, i+1, endi);
> }
> }
> 
> int main(){
> int a[MAX] = {12, 11, 10, 8, 5, 6, 7, 9, 11, 12, 13, 20, 50};
> findBreakpoint(a, 0, MAX-1);
> 
> return 0;
> }