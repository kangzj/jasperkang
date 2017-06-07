---
title: '[CI] Bulb Switcher'
id: 2023
categories:
  - Programming
date: 2015-12-22 09:57:35
tags:
---

&nbsp;
> There are _n_ bulbs that are initially off. You first turn on all the bulbs. Then, you turn off every second bulb. On the third round, you toggle every third bulb (turning on if it's off or turning off if it's on). For the _n_th round, you only toggle the last bulb. Find how many bulbs are on after _n_ rounds.
It's quite a interesting problem and more like a math problem than a coding one. The direct solution is do the swith round by round and we can get the result at the final round. The time complexity of the direct solution is O(n2). The example code is as follows,
<pre class="lang:java decode:true">public int bulbSwitch(int n) {
		int[] lights = new int[n];
		int cnt = 0;
		int i = 0;
		// initailize the array
		for (i = 0; i &lt; n; i++) {
			lights[i] = 0;
		}
		// do the round toggle
		for (i = 0; i &lt; n; i++) {
			for (int j = i; j &lt; n; j += i + 1) {
				lights[j] = lights[j] == 0 ? 1 : 0;
			}
		}
		// get the result
		for (i = 0; i &lt; n; i++) {
			cnt += lights[i];
		}
		return cnt;
}</pre>
Seems like a perfect answer which definitely is not. When I submitted the above code on LeetCode OJ, the platform threw out an error of RUNNING TIME OUT. So it's time to get the code optimized.

As you can see, each one of the bulb is turned on or off for n times which is the number of divisors. But still this cannot solve our problem for the time complexity is O(n2) too! What about printing the result to see whether there is a pattern? Let do it.

when n=40, the result is 100**10000**1000000**100000000**10000000000**10000 . **And when n=60, the result is 100**10000**1000000**100000000**10000000000**1000000000000**100000000000 .

What do you see, guys? Yes, the mumber of each group which has only one 1 is an Arithmetic sequence. So we can get the final result without any toggling rounds. A half but passed solution is as follows,
<pre class="lang:java decode:true ">public int bulbSwitch(int n) {
		int cnt = 0;
		for (int i = 3; n &gt; 0; i += 2) {
			n -= i;
			cnt++;
		}
		return cnt;
}</pre>
That's it.

The time complexity of the above code is O(n) and the code can pass the OJ's test. But is this the most optimized one? No, of course. If you know more maths, the above code can be optimized to the time complexity of O(1) which means there is some formula to get the final result. Can you figure it out, buddy?

By the way, the Ultimate answer is  SQRT(n).

source page: [https://leetcode.com/problems/bulb-switcher/](https://leetcode.com/problems/bulb-switcher/)