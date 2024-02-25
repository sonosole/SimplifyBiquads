# Simplify Biquads

常会遇到双二阶形式的模拟传递函数

$$
H(s) = \frac{\beta_0 + \beta_1 s^{1} + \beta_2 s^{2}} {\alpha_0 + \alpha_1 s^{1} + \alpha_2 s^{2}} \tag{1}
$$

我们希望将其数字化为如下形式

$$
H[z] = \frac{b_0 + b_1 z^{-1} + b_2 z^{-2}} {a_0 + a_1 z^{-1} + a_2 z^{-2}} \tag{2}
$$

这时便需要使用常见的双线性变换

$$
s = \frac{2}{Δt} \frac{1-z^{-1}}{1+z^{-1}} 
  = \frac{Ω}{{\rm tan}(\frac{ω}{2})} \frac{1-z^{-1}}{1+z^{-1}} 
  = k \ \frac{1-z^{-1}}{1+z^{-1}}
$$

其中模拟角频率 $Ω ∈ [0,∞)$ ，数字圆周角频率 $ω ∈ [0,π)$ 。但是直接代入双线性表达式将显得很繁琐，这时我们需要一些化简技巧以简化转换流程。 先观察如下三个直接转换

$$
\begin{align*}
s^2 &= {\color{brown} \frac{k}{1+2\ z^{-1}+z^{-2}}} \ k \ (1-2\ z^{-1}+z^{-2}) \\
s^1 &= k \frac{1 - z^{-1}}{1 + z^{-1}} \frac{1+z^{-1}}{1+z^{-1}} = {\color{brown} \frac{k}{1+2\ z^{-1}+z^{-2}}}(1-z^{-2}) \\
s^0 &= {\color{brown} \frac{k}{1+2\ z^{-1}+z^{-2}}}  {\frac{1+2\ z^{-1}+z^{-2}}{k}}
\end{align*}
$$

去掉公共项，然后替换 $k$ 得到三个替换形式

$$
\begin{align*}
s^2 &\rightarrow \frac{Ω}{{\rm tan}(\frac{ω}{2})} \ (1-2\ z^{-1}+z^{-2}) \\
s   &\rightarrow (1-z^{-2}) \\
1   &\rightarrow  \frac{ {\rm tan}(\frac{ω}{2}) }{Ω} (1+2\ z^{-1}+z^{-2})
\end{align*}
$$

再利用 ${\rm tan}(\frac{ω}{2}) = \frac{{\rm sin}(ω)}{1 + {\rm cos}(ω)} = \frac{1 - {\rm cos}(ω)}{{\rm sin}(ω)}$ 得到

$$
\begin{align*}
s^2 &\rightarrow Ω \frac{1 + {\rm cos}(ω)}{{\rm sin}(ω)} \ (1-2\ z^{-1}+z^{-2}) \\
s   &\rightarrow (1-z^{-2}) \\
1   &\rightarrow  \frac{1}{Ω} \frac{1 - {\rm cos}(ω)}{{\rm sin}(ω)} (1+2\ z^{-1}+z^{-2})
\end{align*}
$$

三者都乘以一个公共项 ${\rm sin}(ω)$， 且令 $Ω=1$ 得到

$$
\begin{align*}
s^2 &\rightarrow  (1 + {\rm cos}(ω)) \ (1-2\ z^{-1}+z^{-2}) \tag{a} \\
s   &\rightarrow {\rm sin}(ω) (1-z^{-2})  \tag{b} \\
1   &\rightarrow  (1 - {\rm cos}(ω)) (1+2\ z^{-1}+z^{-2})  \tag{c} 
\end{align*}
$$

进而有

$$
(s^2+1) \rightarrow 2(1 - 2 {\rm cos}(ω) z^{-1} + z^{-2})  \tag{d} 
$$

将替换项 $(\rm a), (\rm b), (\rm c), (\rm d)$ 带入公式 $(1)$ 便可以更容易地得到形如公式 $(2)$ 的结果。
