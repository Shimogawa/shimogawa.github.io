---
title: 实分析作弊纸
categories: 
- Math
- Analysis
tags:
- Math
- Analysis
language: zh-CN
math: true
---

<!-- <h2 style="text-align: center">公式作弊纸</h2> -->

### 0, 1 实数
<p>
    <b>公理1.1：</b> $\N$是良序的，对于所有$\N$的非空子集$A$，$A$中必有最小元素。
</p>
<p>
    <b>定理1.2：数学归纳法</b> 若$P(n)$是一系列命题，如果$P(1)$是真命题，并且如果$P(m)$是真命题能推导出$P(m+1)$是真命题，那么对所有的$n \in \N$，$P(n)$是真命题。
</p>
<p>
    <b>定理1.3：</b>如果$A$和$B$是可数的，那么$A \times B$也是可数的。
</p>
<p>
    <b>推论1.4：</b>$\mathbb{Q}$是可数的。
</p>
<p>
    <b>定理1.5：（康托）</b>对于非空集$A$，$|A| &lt; |\mathcal{P}(A)|$，其中$\mathcal{P}(A)$是幂集。
</p>
<p>
    <b style="color: red;">定理1.6：</b><b>确界原理</b> 如果$S$是有序集，那么对任意的非空子集$E \subset S$，如果$E$有上界，那么必有上确界，如果有下界，那么必有下确界。$\mathbb{Q}$不适用这个原理。
</p>
<p>
    <b>定理1.7：</b>$\forall n \in \N, \forall x \in \R, x \ge 0, \exists ! y \ge 0$使得$y^n = x$。
</p>
<p>
    <b style="color: red;">定理1.8：</b><b>阿基米德性质</b> $\forall x &gt; 0, y \in \R, \exists n \in \N$使得$nx > y$。
</p>
<p>
    <b>推论1.9：稠密性</b> $\mathbb{Q}$在$\R$中稠密，即$\forall x &lt; y \in \R, \exists q \in \mathbb{Q}$使得$x &lt; q &lt; y$。
</p>
<p>
    <b>定理1.10：</b>如果$S \subset \R$，并且$S$有上界，令$M = \sup S$，那么有$\forall \varepsilon > 0, \exists x \in S$使得$M - \varepsilon &lt; x &lt; M$。
</p>
<p>
    <b>定理1.11：（三角不等式）</b>$|x+y| \le |x| + |y|$。$\big ||x|-|y| \big | \le |x-y|$。
</p>
<p>
    <b>定理1.12：（康托）</b>$\R$是不可数的。
</p>
<br><br>
<hr>

### 2 数列
<p>
    <b style="color: red;">定义2.1：</b><b>数列收敛</b> 数列$x_n$趋向于或收敛于$x$的定义为$\forall \varepsilon > 0, \exists N \in \N$使得$|x_n - x| &lt; \varepsilon, \forall n \ge N$。
</p>
<p>
    <b>定理2.2：</b>收敛数列有界，并且有且仅有一个极限。
</p>
<p>
    <b>技巧2.3：</b>要证明数列不收敛，找到两个子列$\{\overline{x_{n_k}}\}$和$\{\widetilde{x_{n_k}}\}$使得这两个数列收敛于不同极限。
</p>
<p>
    <b>推论2.4：</b>$x_n \rightarrow x$的充要条件是任意子列$\{x_{n_k}\}$也都收敛于$x$。
</p>
<p>
    <b style="color: red;">定理2.5：</b>单调有界数列必定收敛。如果单调递增，那么$x_n \rightarrow \sup \{x_n\}$；如果单调递减，那么$x_n \rightarrow \inf \{x_n\}$。
</p>
<p>
    <b>推论2.6：</b>如果集合$S$有上界，那么存在收敛数列$\{x_n\} \subset S$，并且$x_n \rightarrow \sup S$。
</p>
<p>
    <b>命题2.7：</b>假设$x_n \rightarrow x$，$y_n \rightarrow y$。如果$x_n \le y_n$，那么$x \le y$。
</p>
<p>
    <b style="color: red;">引理2.8：</b><b>夹逼定理</b> 假设$\{x_n\},\{y_n\},\{z_n\}$满足$x_n \le z_n \le y_n$。如果$x_n \to L$，$y_n \to L$，那么$z_n$也收敛于$L$。
</p>
<p>
    <b style="color: red;">定理2.9：</b><b>比较审敛法</b> 令$a_n \ge 0$并且$a_n \to 0$。如果$\{x_n\}$对于足够大的$n$有$|x_n - x| \le a_n$，那么$\{x_n\}$收敛于$x$。
</p>
<p>
    <b>命题2.10：</b>如果$x_n$无界并且单调递增/递减，那么$x_n \to \infty$或$x_n \to -\infty$。
</p>
<p>
    <b style="color: red;">定理2.11：</b><b>比值审敛法</b> 对数列$\{x_n\}$，如果
</p>
<ol>
    <li>
        $\displaystyle \lim_{n\to \infty} \frac{|x_{n+1}|}{|x_n|} &lt; 1$，那么$x_n \to 0$。
    </li>
    <li>
        $\displaystyle \lim_{n\to \infty} \frac{|x_{n+1}|}{|x_n|} &gt; 1$，那么$x_n$发散。
    </li>
    <li>
        $\displaystyle \lim_{n\to \infty} \frac{|x_{n+1}|}{|x_n|} = 1$，那么收敛性不确定。
    </li>
</ol>
<p>
    <b style="color: red;">定理2.12：</b><b>BW</b> 所有在$\R$中的有界数列都有收敛子列。
</p>
<p>
    <b>定理2.13：</b>如果数列$\{x_n\}$收敛，那么存在子列$\{\overline{x}_{n_k}\}$使得$\displaystyle \lim_{n \to \infty} \overline{x}_{n_k} = \limsup_{n \to \infty} x_n$。同样，也存在子列$\{\widetilde{x}_{n_k}\}$使得$\displaystyle \lim_{n \to \infty} \widetilde{x}_{n_k} = \liminf_{n \to \infty} x_n$。
</p>
<p>
    <b>推论2.14：</b>如果$\{x_n\}$有界，那么$\{x_n\}$收敛的充要条件是$\liminf x_n = \limsup x_n$。
</p>
<p>
    <b style="color: red;">定义2.15：</b><b>柯西数列</b> $\{x_n\}$是柯西数列，如果$\forall \varepsilon > 0, \exists N \in \N$使得$\forall n \ge N$和$m \ge N$，有$|x_n - x_m| &lt; \varepsilon$。
</p>
<p>
    <b>定理2.16：</b>所有$\R$上的柯西数列都收敛。
</p>
<p>
    <b style="color: red;">定义2.17：</b><b>级数收敛</b> 级数$\Sigma x_n$收敛的充要条件是部分和$\displaystyle S_n = \sum_{k=1}^n x_k$是收敛数列。
</p>
<p>
    <b>定理2.18：p级数</b> p级数$x_n = n^{-p}, p > 1$收敛。调和级数$\displaystyle \sum \frac{1}{n}$发散。
</p>
<p>
    <b style="color: red;">定理2.19：</b>如果$\Sigma x_n$收敛，那么$|x_n| \to 0$。如果$|x_n| \not \to 0$，那么$\Sigma x_n$发散。
</p>
<p>
    <b>定理2.20：</b>如果级数绝对收敛，那么级数收敛。
</p>
<p>
    <b style="color: red;">定理2.21：</b><b>交错级数审敛法</b> 如果$x_n \ge 0$并且$x_n$单调递减，$x_n \to 0$，那么$\Sigma (-1)^n x_n$收敛。
</p>
<p>
    <b style="color: red;">定理2.22：</b><b>级数比值审敛法</b> 如果$x_n$是非零数列并且极限$\displaystyle L = \lim_{n \to \infty} \frac{|x_{n+1}|}{|x_n|}$存在，那么如果$L &lt; 1$，那么级数绝对收敛；如果$L > 1$，级数发散。
</p>
<p>
    <b style="color: red;">定理2.23：</b><b>级数开根审敛法</b> 假设极限$L = \limsup \sqrt[n]{|x_n|}$存在。那么如果$L &lt; 1$，级数$\Sigma x_n$绝对收敛；如果$L>1$，那么级数发散。
</p>
<p>
    <b style="color: red;">定理2.24：</b><b>幂级数</b> 幂级数$\Sigma a_n (x-x_0)^n$有收敛半径$\displaystyle R = \frac{1}{\displaystyle \limsup_{n \to \infty} \sqrt[n]{|a_n|}}$。如果存在，那么当$|x - x_0| &lt; R$时，级数绝对收敛；如果$|x-x_0| > R$，那么级数发散。等于的情况需要另行讨论。
</p>
<p>
    <b>定理2.25：级数极限比较审敛法</b> 如果有$a_n \gt 0, b_n \gt 0$并且$\displaystyle 0 \lt \lim_{n \to \infty} \frac{a_n}{b_n} \lt \infty$，那么$\Sigma a_n$和$\Sigma b_n$同时收敛或发散。
</p>
<br><br>
<hr>

### 3 连续函数
<p>
    <b style="color: red;">定义3.1：</b><b>聚点</b> 设$S \subset \R$。$x \in \R$是$S$的一个聚点，如果$\forall \varepsilon > 0$，集合$(x-\varepsilon, x+\varepsilon) \cap S \backslash \{x\}$非空。
</p>
<p>
    <b>定理3.2：</b>$x$是$S$的聚点的充要条件是$\exists \{x_n\} \subset S \backslash \{x\}$使得$\displaystyle \lim_{n \to \infty} x_n = x$。
</p>
<p>
    <b style="color: red;">定义3.3：</b><b>函数极限</b> 设函数$f: S \to \R$。令$c \in \R$为$S$的一个聚点。如果有$\forall \varepsilon > 0, \exists \delta > 0$使得对所有的$|x-c| &lt; \delta, x \in S$都有$|f(x) - L| &lt; \varepsilon$，那么定义函数极限$\displaystyle L = \lim_{x \to c} f(x)$。注意，如果$L$存在，那么它唯一。
</p>
<p>
    <b style="color: red;">定理3.4：</b>设$f:S \to \R$，$c$是$S$的一个聚点。那么$\displaystyle \lim_{x \to c} f(x) = L$的充要条件是$\forall \{x_n\} \subset S \backslash \{x\}$并且$x_n \to c$，都有$\displaystyle \lim_{n \to \infty} f(x_n) = L$。
</p>
<p>
    <b>定理3.5：</b>函数极限存在的充要条件是双侧极限存在且相等。
</p>
<p>
    <b style="color: red;">定义3.6：</b><b>连续性</b> 对于函数$f:S \to \R, c \in S$，如果有$\forall \varepsilon > 0, \exists \delta = \delta(\varepsilon, c) > 0$使得$\forall x \in S, |x - c| &lt; \delta$都有$|f(x) - f(c)| &lt; \varepsilon$，那么$f$在$c$连续。如果对所有$c \in S$，$f$都连续，那么我们说$f$在$S$上连续。
</p>
<p>
    <b style="color: red;">定理3.7：</b>$f$在$c$连续的充要条件是$\forall x_n \to c, x_n \in S$，都有$f(x_n) \to f(c)$。
</p>
<p>
    <b>推论3.8：</b>$f(x) = x^r, r \in \mathbb{Q}$是连续的。
</p>
<p>
    <b>定理3.9：</b>若有$f: A \to B, g: B \to \R$，并且$f$在$c$连续，$g$在$f(c)$连续，那么复合函数$h = g \circ f : A \to \R$在$c$连续（$h(x) = g(f(x))$）。
</p>
<p>
    <b style="color: red;">定理3.10：</b>如果存在数列$\{x_n\} \subset S$，$x_n \to c$但是$f(x_n) \not \to c$，那么$f$在$c$不连续。
</p>
<p>
    <b style="color: red;">定理3.11：</b><b>最大最小值定理</b> 如果$f: [a,b] \to \R$是连续的，那么$f$有界，并且在$[a,b]$上有最大最小值。
</p>
<p>
    <b style="color: red;">引理3.12：</b><b>零点定理</b> 如果$f: [a,b] \to \R$是连续的，并且$f(a) &lt; 0$，$f(b) > 0$，那么存在$c \in (a,b)$使得$f(c) = 0$。
</p>
<p>
    <b style="color: red;">定理3.13：</b><b>介值定理，中间值定理</b> 如果$f:[a,b] \to \R$连续，并且存在$y$在$f(a)$和$f(b)$之间，那么存在$x_0 \in (a,b)$使得$f(x_0) = y$。
</p>
<p>
    <b>推论3.14：</b>如果$f: [a,b] \to \R$是连续的，那么$f([a,b]) = [\inf f, \sup f]$。
</p>
<p>
    <b>推论3.15：</b>所有奇数次多项式都有一个实根。
</p>
<p>
    <b style="color: red;">定义3.16：</b><b>一致连续性</b> $f$在$S$上一致连续的定义是$\forall \varepsilon > 0, \exists \delta = \delta(\varepsilon) > 0$使得$\forall |x - y| &lt; \delta$都有$|f(x) - f(y)| &lt; \varepsilon$。
</p>
<p>
    <b>定理3.17：</b>一致连续的函数是连续的。
</p>
<p>
    <b>定理3.18：</b>如果$f:[a,b] \to \R$连续，那么$f$在$[a,b]$上一致连续。
</p>
<p>
    <b>定理3.19：</b>如果$\{x_n\} \subset S$是柯西数列，并且$f$在$S$上一致连续，那么$\{f(x_n)\}$也是柯西数列。
</p>
<p>
    <b>定理3.20：</b>一致连续性的推广略。（暂时）
</p>
<p>
    <b style="color: red;">定义3.21：</b><b>利普希茨连续</b> 如果对于函数$f: S \to \R$，存在$M > 0$使得对于任意的$x,y \in S$，都有$|f(x) - f(y)| \le M |x-y|$，那么函数$f$是Lipschitz连续的。
</p>
<p>
    <b>定理3.22：</b>Lipschitz连续函数是一致连续的。
</p>
<p>
    <b style="color: red;">定义3.23：</b><b>单调性</b> 如果$f$满足$x \lt y \Rightarrow f(x) \le f(y)$，那么$f$是单调递增的。如果$f$满足$x \lt y \Rightarrow f(x) \ge f(y)$，那么$f$是单调递减的。严格递增递减是将等号去除的情况。
</p>
<p>
    <b>定理3.24：</b>如果$I \subset \R$是一个区间，并且$f: I \to \R$是严格单调的，那么$f(I)$是一个区间的充要条件是$f$是连续的。
</p>
<p>
    <b>定理3.25：</b>如果$f: I \to \R$是单调的，那么$f$有最多可数无穷个间断点（不连续点）。
</p>
<br><br>
<hr>

### 4 导数
<p>
    <b style="color: red;">定义4.1：</b><b>导数</b> 若函数$f:I \to \R$，$c \in I$是一个聚点。如果极限$\displaystyle L = \lim_{x \to c} \frac{f(x) - f(c)}{x-c}$存在，那么我们称$f$在$c$可导，并且$L$叫做$f$在$c$的导数，记作$f'(c) = L$。
</p>
<p>
    <b>定理4.2：</b>可导必连续。
</p>
<p>
    <b>定理4.3：链式法则</b> 若$f:I_1 \to I_2$在$c \in I_1$可导，$g:I_2 \to \R$在$f(c) \in I_2$可导，那么$g \circ f: I_1 \to \R$在$c$可导，并且导数$(g \circ f)'(c) = g'(f(c)) \cdot f'(c)$。
</p>
<p>
    <b>定理4.4：</b>如果函数$f: I \to \R$在$c$可导，并且在$c$有局部极值，那么$f'(c) = 0$。
</p>
<p>
    <b>定义4.5：</b>驻点指导数为$0$的点。
</p>
<p>
    <b>定理4.6：</b>假设$f: [a,b) \to \R$是连续的并且在$(a,b)$上可导。如果$\displaystyle \lim_{x \to a^+} f'(x)$存在并等于$L$，那么说$f$在$a$可导，并且$f'(a) = L$。
</p>
<p>
    <b style="color: red;">定理4.7：</b><b>罗尔定理</b> 假设$f: [a,b] \to \R$是连续的，并且在$(a,b)$上可导。如果$f(a) = f(b)$，那么存在$c \in (a,b)$使得$f'(c) = 0$。
</p>
<p>
    <b style="color: red;">定理4.8：</b><b>中值定理</b> 假设$f: [a,b] \to \R$是连续的，并且在$(a,b)$上可导，那么存在$c \in (a,b)$使得$\displaystyle f'(c) = \frac{f(b) - f(a)}{b-a}$，或$f(b) - f(a) = f'(c)(b-a)$。
</p>
<p>
    <b>推论4.9：</b>如果$f'(x) = 0, \forall x$，那么$f$是常值函数。如果$f'(x) \ge 0$，那么$f$单调递增。反之亦然。
</p>
<p>
    <b>定理4.10：一阶导数测试</b> 假设$f:(a,b) \to \R$在$(a,b) \backslash \{c\}, c \in (a,b)$上是连续并可导的。如果在$(a,c)$上$f'(x) \le 0$，并且在$(c,b)$上$f'(x) \ge 0$，那么$f$在$c$有最小值。反之亦然。
</p>
<p>
    <b style="color: red;">定理4.11：</b><b>洛必达法则</b> 假设$f,g:(a,b) \to \R$是可导的，$c \in (a,b)$。如果$f(c) = g(c) = 0, g'(x) \ne 0$，并且极限$\displaystyle L = \lim_{x \to c} \frac{f'(x)}{g'(x)}$存在，那么$\displaystyle \lim_{x \to c} \frac{f(x)}{g(x)} = L$。
</p>
<p>
    <b style="color: red;">定理4.12：</b><b>达布中值定理</b> 假设$f:[a,b] \to \R$是可导的。如果有$y$在$f'(a)$和$f'(b)$之间，那么存在$c \in (a,b)$使得$f'(c) = y$。
</p>
<p>
    <b style="color: red;">定理4.13：</b><b>泰勒展开</b> 假设$f:[a,b] \to \R$是$n$阶连续可导的并且$n+1$阶导数存在。给定$x_0 \in [a,b]$，对任意$x \ne x_0 \in [a,b]$，存在$c \in (a,b)$在$x$与$x_0$之间，使得
    \[f(x) = P_n^{x_0}(x) + R_n^{x_0}(x),\]
    其中$\displaystyle P_n^{x_0}(x) = \sum_{k=0}^n \frac{f^{(k)}(x_0)}{k!} (x-x_0)^k$称为泰勒多项式，$\displaystyle R_n^{x_0}(x) = \frac{f^{(n+1)}(c)}{(n+1)!} (x-x_0)^{n+1}$称为拉格朗日余项。
</p>
<p>
    <b>定理4.14：二阶导数测试</b> 假设$f$在$(a,b)$上有二阶连续导数，并且$x_0 \in (a,b)$是一个驻点，即$f'(x_0) = 0$。如果$f''(x_0) \gt 0$，那么$f$在$x_0$是局部最小值。反之亦然。
</p>
<br><br>
<hr>

### 5 黎曼积分
<p>
    <b>定义5.1：划分</b> 如果有$a = x_0 \lt x_1 \lt ... \lt x_n = b$，那么称$P = \{x_0, x_1, ..., x_n\}$是在区间$[a,b]$上的一个划分，并且，记$\Delta x_i = x_i - x_{i-1}$。对于一个在这个划分上的函数$f(x)$，记$\displaystyle m_i = \inf_{[x_{i-1}, x_i]} f(x)$，$\displaystyle M_i = \sup_{[x_{i-1}, x_i]} f(x)$。
</p>
<p>
    <b>定义5.2：上下达布和</b> 对于一个划分$P$，定义上达布和$\displaystyle U(P, f) = \sum_{i=1}^n M_i \Delta x_i$，和下达布和$\displaystyle L(P, f) = \sum_{i=1}^n m_i \Delta x_i$。
</p>
<p>
    <b>定义5.3：上下积分</b> 设$P$为划分，定义上积分$\displaystyle \overline \int^b_a f = {\inf}_P U(P, f)$，下积分$\displaystyle \underline {\int}^b_a f$。
</p>
<p>
    <b style="color: red;">定义5.3：</b><b>黎曼可积</b> 函数$f: [a,b] \to \R$是黎曼可积的，如果$f$有界并且$\displaystyle \overline \int^b_a f = \underline {\int}^b_a f = \int^b_a f$。我们称$\displaystyle \int^b_a f$为黎曼积分，并且记$\displaystyle \int^b_a f = \int^b_a f(x) dx$。如果$f$在$[a,b]$上黎曼可积，记作$f \in \mathscr{R} [a,b]$。
</p>
<p>
    <b style="color: red;">定理5.4：</b> $f:[a,b] \to \R$是黎曼可积的充要条件是对于任意$\varepsilon > 0$，存在一个划分$P$使得$0 \le U(P, f) - L(P, f) \lt \varepsilon$。
</p>
<p>
    <b>定义5.5：Refinement</b> 我们称$\widetilde P$是划分$P$的Refinement，如果$P \subset \widetilde P$。
</p>
<p>
    <b>推论5.6：</b> 假设$P_1$和$P_2$是在$[a,b]$上的划分，那么$P = P_1 \cup P_2$是$P_1$和$P_2$的Refinement，并且有$L(P_1,f) \le L(P,f) \le U(P,f) \le U(P_2,f)$。
</p>
<p>
    <b>命题5.7：</b> 如果$m \le M$，那么$m(b-a) \le L(P,f) \le U(P,f) \le M(b-a)$。
</p>
<p>
    <b style="color: red;">定理5.8：</b> 如果$f:[a,b] \to \R$是连续的，那么它是黎曼可积的。
</p>
<p>
    <b>推论5.9：</b> 假设$f$是连续的并且$f \ge 0$。如果$\int_a^b f = 0$，那么$f(x) = 0, \forall x$。
</p>
<p>
    <b style="color: red;">定理5.10：</b> 如果$f:[a,b] \to \R$是单调的，那么$f$是黎曼可积的。
</p>
<p>
    <b>定理5.11：</b> 假设$f:[a,b] \to \R$有界并且数列$a_n$单调递减，$a_n \to a$，数列$b_n$单调递增并且$b_n \to b$。如果对于所有的$n \in \N$，$f$在$[a_n, b_n]$是黎曼可积的，那么$f$在$[a,b]$上是黎曼可积的，并且$\displaystyle \int^b_a f = \lim_{n \to \infty} \int^{b_n}_{a_n} f$。
</p>
<p>
    <b>定理5.12：</b> 如果$f$有界并且$f$有有限个间断点，那么$f$是黎曼可积的。
</p>
<p>
    <b style="color: red;">定理5.13：微积分基本定理1 牛顿-莱布尼茨公式</b> 假设$F$在$[a,b]$上连续，并且在$(a,b)$上可导，令$f = F'$。如果$f \in \mathscr R[a,b]$，那么$\displaystyle \int^b_a f = F(b) - F(a)$。
</p>
<p>
    <b style="color: red;">定理5.14：微积分基本定理2</b> 假设$f \in \mathscr R [a,b]$，并且$x \in [a,b]$。定义$\displaystyle F(x) = \int^x_a f$，那么$F$在$[a,b]$上连续。如果$f \in C^0[a,b]$（$C^n[a,b]$指$n$阶连续可导），那么$F$在$[a,b]$上可导，并且$F'(c) = f(c)$。
</p>
<p>
    <b>定理5.15：换元法</b> 假设$g \in C^1[a,b]$，并且$g([a,b]) \subset [c,d]$，令$f \in C^0 [c,d]$，那么有$\displaystyle \int^b_a f(g(x)) g'(x) dx = \int^{g(b)}_{g(a)} f(s) ds$。
</p>
<p>
    <b>定理5.16：自然对数函数</b> 存在唯一的函数$L: (0, +\infty) \to \R$，并且有以下性质：
</p>
<ol>
    <li>
        $L(1) = 0$；
    </li>
    <li>
        $\displaystyle L'(x) = \frac{1}{x}$；
    </li>
    <li>
        $L$是严格单调递增并且是双射，并且有$\displaystyle \lim_{x \to 0^+} L(x) = -\infty$，$\displaystyle \lim_{x \to \infty} L(x) = +\infty$；
    </li>
    <li>
        $L(xy) = L(x) + L(y)$；
    </li>
    <li>
        对于任意$q \in \mathbb{Q}$，有$L(x^q) = qL(x)$。
    </li>
</ol>
<p>
    函数$L$又能记作$\ln(x)$或$\log(x)$。
</p>
<p>
    <b>定理5.17：自然对数函数幂级数展开</b> $\displaystyle \ln(x+1) = \sum_{k = 1}^\infty \frac{x^k}{k!}(-1)^{k-1}$。 
</p>
<p>
    <b>定理5.18：自然指数函数</b> 存在唯一的函数$E: \R \to (0, +\infty)$，并且有以下性质：
</p>
<ol>
    <li>
        $E(0) = 1$；
    </li>
    <li>
        $E$是双射，严格递增，并且$\displaystyle \lim_{x \to -\infty} E(x) = 0$，$\displaystyle \lim_{x \to \infty} E(x) = +\infty$；
    </li>
    <li>
        $E(x+y) = E(x)E(y)$；
    </li>
    <li>
        对于任意$q \in \mathbb{Q}$，$E(qx) = E(x)^q$。
    </li>
</ol>
<p>
    函数$E$又能记作$\exp(x)$。
</p>
<p>
    <b>定义5.19：自然常数</b> 欧拉常数$e = E(1)$。并且，令$E(x) = e^x = exp(x)$等价。
</p>
<p>
    <b>定义5.20：</b> 对于任意$x>0$和$y \in \R$，定义$x^y = \exp(y \ln x)$。
</p>
<p>
    <b>定理5.21：自然指数函数幂级数展开</b> $\displaystyle e^x = \sum^\infty_{k = 0} \frac{x^k}{k!}$。
</p>
<p>
    <b>定义5.22：反常积分</b> 假设$f$在所有$c \in (a,b)$黎曼可积，并且$\displaystyle \lim_{c \to b^-} \int^c_a f$存在，那么定义反常积分$\displaystyle \int^b_a f = \lim_{c \to b^-} \int^c_a f$。
</p>
<p>
    <b>定理5.23：反常积分的p级数审敛法</b> 
</p>
<ol>
    <li>
        若$p \gt 1$，那么$\displaystyle \int^\infty_1 \frac{1}{x^p} dx = \frac{1}{p-1}$。
    </li>
    <li>
        若$p \lt 1$，那么$\displaystyle \int^1_0 \frac{1}{x^p} dx = \frac{1}{1-p}$。
    </li>
</ol>
<p>
    <b style="color: red;">定理5.24：积分比较审敛法</b> 若$f: [a,\infty) \to \R, g : [a, \infty) \to \R$，并且对于任意的$x$，都有$|f(x)| \le g(x)$，那么
</p>
<ol>
    <li>
        如果$\int^\infty_a g$存在，那么$\int^\infty_a f$也存在，并且$| \int^\infty_a f | \le \int^\infty_a g$。
    </li>
    <li>
        如果$\int^\infty_a f$发散，那么$\int^\infty_a g$也发散。
    </li>
</ol>
<p>
    <b>定理5.25：级数的积分审敛法</b> 假设$f: [k, +\infty) \to \R$非负并且单调递减。那么，$\displaystyle \sum_{n \ge k} f(n)$收敛的充要条件是$\displaystyle \int^\infty_k f$收敛，并且如果$\displaystyle \int^\infty_k f \le \infty$，有$\displaystyle \int^\infty_k f \le \sum_{n \ge k} f(n) \le f(k) + \int^\infty_k f$。
</p>
<br><br>
<hr>

### 6 函数列
<p>
    <b>定义6.1：点收敛</b> 假设有函数列${f_n}_{n \ge 1} : S \to \R$。如果对于$f: S \to \R$，有对任意的$x \in S$，$\displaystyle \lim_{n \to \infty} f_n(x) = f(x)$，那么称$f_n$点收敛于$f$。
</p>
<p>
    <b>定义6.2：一致收敛</b> 函数列$f_n$一致收敛于$f$，如果对于任意的$\varepsilon > 0$，都存在$N \in \N$，使得对任意的$n \ge N$和$x \in S$，有$|f_n(x) - f(x)| \lt \varepsilon$。
</p>
<p>
    <b>定义6.3：一致范数</b> 假设$f: S \to \R$有界，定义$f$在$S$上的一致范数为$\displaystyle \|f\|_u = \|f\|_{L^\infty(S)} = \sup_{x \in S} |f(x)|$。
</p>
<p>
    <b style="color: red;">定理6.4：一致收敛</b> 函数列$f_n$一致收敛于$f$的充要条件是$\displaystyle \lim_{n \to \infty} \|f_n - f\|_u = 0$。
</p>
<p>
    <b>性质6.5：</b> $\|f+g\|_u \le \|f\|_u + \|g\|_u$。
</p>
<p>
    <b>推论6.6：</b> 如果$f_n$在$S$上一致收敛于$f$，那么$f_n$在$S$上点收敛于$f$。
</p>
<p>
    <b>定义6.7：一致柯西收敛</b> 如果有界函数列$f_n: S \to \R$有$\forall \varepsilon \gt 0, \exists N$使得对任意的$n, m \ge N$，$\|f_n - f_m\|_u \lt \varepsilon$，那么称$f_n$在$S$上一致柯西收敛。
</p>
<p>
    <b>推论6.8：</b> 函数列一致柯西收敛的充要条件是函数列一致收敛。
</p>
<p>
    <b>定理6.9：</b> 假设连续有界函数列$f_n: S \to \R$在$S$上一致收敛于$f$，那么$f$也是连续且有界的。
</p>
<p>
    <b style="color: red;">定理6.10：</b> 假设$f_n \in \mathscr R[a,b]$，并且$f_n$在$[a,b]$上一致收敛于$f$，那么$f \in \mathscr R[a,b]$，并且$\displaystyle \lim_{n \to \infty} \int^b_a f_n = \int^b_a f$。
</p>
<p>
    <b style="color: red;">定理6.11：</b> 假设存在有界区间$I$，并且$f_n \in C^1(I)$，那么如果
</p>
<ol>
    <li>
        存在$c \in I$使得$f_n(c)$收敛于某个数，
    </li>
    <li>
        存在$g \in C^1(I)$使得$f_n' \to g$在$I$上一致收敛，
    </li>
</ol>
<p>
    那么存在$f \in C^1(I)$，并且$f' = g$，使得$f_n$在$I$上一致收敛于$f$。
</p>
<p>
    <b>定理6.12：幂级数</b>
</p>
<br><br>
<hr>

### 7 度量空间
<p>
    <b>定义7.1：</b> 定义度量空间$(X,d)$，其中$X$是集合，映射$d: X \times X \to [0, +\infty)$称作度量，并且满足
</p>
<ol>
    <li>
        <b>正定性：</b> $d(x,y) \ge 0$，并且当且仅当$x=y$时$d(x,y) = 0$。
    </li>
    <li>
        <b>对称性：</b> $d(x,y) = d(y,x)$。
    </li>
    <li>
        <b>三角不等式：</b> $d(x,y) \le d(x, z) + d(z, y)$。
    </li>
</ol>
<p>
    <b style="color: red;">定理7.2：柯西施瓦茨不等式</b> 假设向量$\b a, \b b \in \R^n$，那么$\b a \cdot \b b \le \|\b a\| \|\b b\|$。
</p>
<p>
    <b>定义7.3：有界性</b> 非空度量空间$S \subset (X,d)$有界的定义是存在$p \in X$和$M \gt 0$使得对任意的$x \in S$，都有$d(p, x) \le M$。定义半径$\text{diam}(S) = \sup \{d(x,y): x,y \in S\}$。
</p>
<p>
    <b>定理7.4：</b> $S \ne \emptyset$有界的充要条件是$\text{diam}(S) \lt \infty$。
</p>
<p>
    <b>定义7.5：开球与闭球</b> 开球$B(x,r) = \{y \in X: d(x,y) \lt r\}$。闭球$C(x,r) = \{y \in X: d(x,y) \le r\}$。
</p>
<p>
    <b>定义7.6：开、闭集</b> 集合$A \subset (X,d)$是开集，如果$\forall x \in A, \exists \varepsilon > 0$使得$B(x,\varepsilon) \subset A$。如果$A^C$是开集，那么称$A$是闭集。
</p>
<p>
    <b>推论7.7：</b> 对于度量空间$(X,d)$，
</p>
<ol>
    <li>
        $\emptyset$和$X$是闭开集，即又开又闭的集合。
    </li>
    <li>
        任意开集的并集是开集。
    </li>
    <li>
        有限个开集的交集是开集。
    </li>
    <li>
        有限个闭集的并集是闭集。
    </li>
    <li>
        任意闭集的交集是闭集。
    </li>
</ol>
<p>
    <b>定理7.8：</b> 在度量空间$(X,d)$中，开球$B(x, \varepsilon)$是开集，闭球$C(x,\varepsilon)$是闭集。
</p>
<p>
    <b>定义7.9：闭包（Closure）</b> 定义集合$A \subset (X,d)$的闭包为包含$A$的最小闭集，即$\overline{A} = \cap_{F \text{ closed, } F \subset A} F$。 
</p>
<p>
    <b>性质7.10：闭包的性质</b>
</p>
<ol>
    <li>
        $A \subset \overline A$。
    </li>
    <li>
        $\overline A$是闭集。
    </li>
    <li>
        $A$是闭集当且仅当$A = \overline A$。
    </li>
    <li>
        $x \in \overline A$当且仅当$\forall \varepsilon > 0, B(x, \varepsilon) \cap A \ne \emptyset$。
    </li>
</ol>
<p>
    <b>定义7.11：内部（Interior）</b> 定义集合$A$的内部为$A$的最大开子集，即$A^\circ = \cup_{E \text{ open, } E \subset A} E$。
</p>
<p>
    <b>性质7.12：内部的性质</b>
</p>
<ol>
    <li>
        $A^\circ \subset A$。
    </li>
    <li>
        $A^\circ$是开集。
    </li>
    <li>
        $A$是开集当且仅当$A = A^\circ$。
    </li>
    <li>
        $x \in A^\circ$当且仅当$\exists \varepsilon > 0$使得$B(x,\varepsilon) \subset A$。
    </li>
</ol>
<p>
    <b>定义7.13：边界</b> 集合$A$的边界是$\partial A = \overline A \backslash A^\circ$。
</p>
<p>
    <b>推论7.14：</b> $x \in \partial A$的充要条件是$\forall \varepsilon > 0, B(x, \varepsilon) \cap A \ne \emptyset$并且$B(x,\varepsilon) \cap A^C \ne \emptyset$。
</p>
<p>
    <b>定义7.15：连通集</b> 如果非空度量空间$(X, d)$的闭开子集只有$\emptyset$和$X$自身，那么称它为连通集。
</p>
<p>
    <b>定义7.16：不连通集</b> 在度量空间$(X,d)$中，假设$S \subset X$。如果在$X$中存在开集$U_1$和$U_2$，使得$U_1 \cap U_2 \cap S = \emptyset$，$U_1 \cap S \ne \emptyset$，$U_2 \cap S \ne \emptyset$，并且$S = (U_1 \cap S) \cup (U_2 \cap S)$，那么称$S$为不连通集。
</p>
<p>
    <b>定义7.17：子空间</b> 令$Y \subset X$使得$(Y,d)$是$(X,d)$的子空间。那么，$U$在$(Y,d)$中是开集的充要条件是存在开集$V \subset (X,d)$使得$U = V \cap Y$。
</p>
<p>
    <b>定义7.18：开覆盖</b> 集合$K \subset X$的一个开覆盖是对任意开集$U_\lambda$，$\displaystyle U = \{U_\lambda : K \subset \bigcup_\lambda U_\lambda\}$。
</p>
<p>
    <b>定义7.19：紧致集</b> 若集合$K \subset X$的任意开覆盖存在有限子覆盖，则称$K$是紧致集，或紧集。即，存在有限集合$\{\lambda_1, \lambda_2, ..., \lambda_k\}$使得$K \subset \bigcup^k_{i = 1} U_{\lambda_i}$。
</p>
<p>
    <b>定理7.20：（A）</b> 紧致集是有界闭集。
</p>
<p>
    <b>定理7.20：（B）数列紧致</b> $K \subset (X,d)$是紧致集的充要条件是对于任意的$\{x_n\} \subset K$，存在$\{x_{n_i}\} \subset \{x_n\}$使得$x_{n_i}$收敛于$x \in K$。
</p>
<p>
    <b>定理7.20：（C）</b> 如果$K$是紧致的，并且$E$是闭集，那么$K \cap E$是紧致的。
</p>
<p>
    <b>定理7.20：（D）海涅-博雷尔定理</b> 集合$K \subset \R^n$是紧致集的充要条件是$K$是有界闭集。
</p>