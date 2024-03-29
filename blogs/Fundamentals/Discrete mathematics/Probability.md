# 概率论

----
### 概率指派
* 基础：概率分布（离散、连续）

### 事件组合
* 事件与其补事件的概率和为1。
* 两个事件之一发生概率等于两个事件分别发生概率之和减去两者同时发生的概率。（类似容斥原理）

### 条件概率
* P(E|F) = P(E(and)F) / P(F)
* 如果P(E|F) = P(E)，那么E和F事件独立。等价于P(E(and)F)=P(E)P(F)。

### 伯努利与二项分布
* n次独立伯努利实验中，每次成功概率为p，失败为q=1-p，那么正好k次成功的概率是：C(n, k)(p^k)(q^(n-k))

----
### 贝叶斯定理


----
### 期望和方差
* 期望定义：E(X) = ∑(p(s)X(s))
* 期望性质：关于变量是线性的。
* 方差定义：V(X) = ∑(p(s)(X(s)-E(X))^2)
* 切比雪夫不等式：p(|X(s)-E(X)|>=r) <= V(X)/r^2。其中X为随机变量，r是正实数。
