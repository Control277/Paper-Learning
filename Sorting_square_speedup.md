总元素：**n**
并行度：**p**
复杂度：**R**
排序算法：选择排序，$O(n^2)$

则单线程排序复杂度为
$
R_{single} = n^2
$

多线程排序，采用先分组，后归并算法
* 每个线程排序复杂度为
$
R_{thread} = N^2={(\frac{n}{p})^2}=\frac{n^2}{p^2}
$
* 归并即每一轮从p个子数组取最小的一个放入结果数组，执行n次，复杂度为
$
R_{reduce} = np
$

则多线程排序总的时间为
$
R_{multi}=\frac{n^2}{p^2} + np
$

多线程相比于单线程的加速比为
$
Speedup= \frac{R_{single}}{R_{multi}}=\frac{n^2}{\frac{n^2}{p^2} + np}
$
考虑到$n \gg p$，则求极限$n\to\infty$
$
Speedup= \lim_{n\to\infty} \frac{n^2}{\frac{n^2}{p^2} + np}
=\lim_{n\to\infty} \frac{n^2p^2}{n^2 + np^3}
=\lim_{n\to\infty} \frac{p^2}{1 + \frac{p^3}{n}}
=p^2
$
即**多线程排序的加速比为并行度的平方**

