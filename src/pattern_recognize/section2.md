## 习题2

#### 2.1

如果只知道各类的先验概率，最小错误率贝叶斯决策规则应如何表示？

解答：由于只知道先验概率，那么任何的观测值都不能起到作用，也就是说

$$
p(\omega_i|x) = P(\omega_i)
$$

#### 2.2

利用概率论中的乘法定理和全概率公式证明贝叶斯公式

$$
p(\omega_i| x) = \frac{p(x|\omega_i)P(\omega_i)}{p(x)}
$$

解答：

$$
p(\omega_i|x) =\frac {P(\omega_i, x)}{p(x)} =  \frac{p(x|\omega_i)P(\omega_i)}{p(x)}
$$

#### 2.3

证明：在两类情况下 $P(\omega_1|x) + P(\omega_2|x) = 1$。

解答：

$$
\begin{aligned}
P(\omega_1|x) + P(\omega_2|x) &=\frac {P(\omega_1, x)}{p(x)} + \frac{P(\omega_2, x)}{p(x)}\\
&= \frac{p(x)}{p(x)} = 1
\end{aligned}
$$

#### 2.4

分别写出在以下两种情况
$$
\begin{aligned}
&(1) P(x|\omega_1) = P(x|\omega_2)\\
&(2) P(\omega_1) = P(\omega_2)
\end{aligned}
$$

下的最小错误率贝叶斯决策规则。

解答：

(1)

$$
P(\omega_1) \gtrless P(\omega_2) => x \in \left\{\begin{aligned}\omega_1\\\omega_2\end{aligned}\right.
$$

(2) 类似

#### 2.5

(1) 对 c 类情况推广最小错误率贝叶斯决策规则；

(2) 指出此时使错误率最小等价于后验概率最大，即

$$
p(\omega_i|x) > p(\omega_j|x)
$$

对一切 $j \ne i$ 成立时 $x \in \omega_i$ 。

解答：

(1) 若对于任意的 $j = 1,2,,c$，都有 $p(\omega_i|x) > p(\omega_j|x)$ ，那么 $x \in \omega_i$

(2) 显然的

#### 2.6

对于两类问题，证明最小风险贝叶斯决策规则可表示为，若

$$
\frac{p(x|\omega_1)}{p(x|\omega_2)} \gtrless \frac{(\lambda_{12} - \lambda_{22})P(\omega_2)}{(\lambda_{21} - \lambda_{11})P(\omega_1)} => x\in\left\{\begin{aligned}\omega_1\\\omega_2\end{aligned}\right.
$$

解答：

根据定义，条件风险

$$
R(a_i |x) = \sum \lambda(a_i,\omega_j) p(\omega_j|x)=\sum \lambda(a_i,\omega_j)\frac{p(x|\omega_j)P(\omega_j)}{p(x)}
$$

而对于两类情况，最小风险贝叶斯决策规则为

$$
R(a_1|x) \lessgtr R(a_2|x) =>x \in \left\{\begin{aligned}\omega_1 \\\omega_2\end{aligned}\right.
$$

而

$$
\frac{R(a_1|x)}{R(a_2|x)} = \frac{\lambda_{11} p(x|\omega_1)P(\omega_1) + \lambda_{12} p(x|\omega_2)P(\omega_2)}{\lambda_{21} p(x|\omega_1)P(\omega_1) + \lambda_{22} p(x|\omega_2)P(\omega_2)}
$$

于是
$$
\begin{aligned}
\frac{R(a_1|x)}{R(a_2|x)} \lessgtr 1 &=> \frac{\lambda_{11} p(x|\omega_1)P(\omega_1) + \lambda_{12} p(x|\omega_2)P(\omega_2)}{\lambda_{21} p(x|\omega_1)P(\omega_1) + \lambda_{22} p(x|\omega_2)P(\omega_2)} \lessgtr 1 \\
&=>(\lambda_{11}-\lambda_{21})p(x|\omega_1)P(\omega_1) \lessgtr (\lambda_{22}-\lambda_{12})p(x|\omega_2)P(\omega_2)\\
&=>(\lambda_{11} - \lambda_{21}) \frac{p(x|\omega_1)}{p(x|\omega_2)} \lessgtr (\lambda_{22} - \lambda_{12}) \frac{P(\omega_2)}{P(\omega_1)}
\end{aligned}
$$

注意上式的 $(\lambda_{11} - \lambda_{21})$ 一般来讲是小于 0 的，为啥？因为预测错误的风险肯定大于预测正确的风险。于是将其移到公式右边肯定要将符号反向，于是便得到证明。

#### 2.7

若 $\lambda_{11} = \lambda_{22} = 0, \lambda_{12} = \lambda_{21}$，证明此时最小最大决策面使得来自两类的错误率相等。

解答：

首先假设类条件概率分别为 $p(\omega_1|x), p(\omega_2|x)$ ，以及两类先验概率 $p(\omega_1), p(\omega_2)$. 依据这一条件, 计算风险期望

$$
\begin{aligned}
R &= \int_A R(a|x)p(x)\mathrm{d}x\\
&= \int_{A_1} R(a_1|x)p(x)\mathrm{d}x + \int_{A_2} R(a_2|x)p(x)\mathrm{d}x \\
&= \int_{A_1} \lambda_{11} p(\omega_1|x)p(x) + \lambda_{12} p(\omega_2|x)p(x)\mathrm{d}x \\&+  \int_{A_2} \lambda_{21} p(\omega_1|x)p(x) + \lambda_{22} p(\omega_2|x)p(x)\mathrm{d}x
\end{aligned}
$$

由于 $\lambda_{11} = \lambda_{22} = 0$ ， 在结合

$$
p(\omega_1) + p(\omega_2) = 1\\
\int_{A_1}p(x|\omega_1) \mathrm{d}x + \int_{A_2} p(x|\omega_1)\mathrm{d}x = 1
$$

上式可以化为

$$
\begin{aligned}
R &= \lambda p(\omega_2)\int_{A_1} p(x|\omega_2)\mathrm{d}x + \lambda p(\omega_1)\int_{A_2}p(x|\omega_1)\mathrm{d}x\\
&= \lambda (1 - p(\omega_1)) \int_{A_1} p(x|\omega_2)\mathrm{d}x + \lambda p(\omega_1) \left[
1 - \int_{A_1} p(x|\omega_1)\mathrm{d}x
\right] \\
&= \lambda \int_{A_1} p(x|\omega_2)\mathrm{d}x - p(\omega_1) \left[
\lambda \int_{A_1} p(x|\omega_2)\mathrm{d}x + \lambda  \int_{A_1} p(x|\omega_1)\mathrm{d}x - \lambda
\right] \\
&=a + b  p(\omega_1)
\end{aligned}
$$

并且 $b=0$ , 于是对于任意的先验概率 $p(\omega_1)$, 其期望风险都是不变的.

#### 2.9

写出两类和多类情况下最小风险贝叶斯决策判别函数和决策面方程

解答：

多类情况下，判别函数为

$$
g_i(x) = p(\alpha_i|x) = \sum_{j=1}^n \lambda_{ij}p(\omega_j|x)
$$

决策面

$$
g_i(x) = g_j(x)
$$

#### 2.10

随机变量  $l(x)$ 定义为

$$
l(x) = \frac{p(x|\omega_1)} {p(x|\omega_2)}
$$

$l(x)$ 又称为似然比，试证明：

(1) $E\{l^n(x) |\omega_1\} =E\{l^{n-1}(x) |\omega_2\}$

(2) $E\{l(x) |\omega_2\} = 1$

(3) $E\{l(x) |\omega_1\} -E\{l(x) |\omega_2\} = Var\{l(x)|\omega_2\}$

解答：

(2)
$$
\begin{aligned}
E\{l(x)|\omega_2\} &= \int l(x)p(x|\omega_2)\mathrm{d}x\\
&= \int p(x|\omega_1)\mathrm{d}x\\
&= \int \frac{p(x,\omega_1)}{p(\omega_1)}\mathrm{d}x\\
&= \frac{1}{p(\omega_1)} \int p(x, \omega_1)\mathrm{d}x\\
&=1
\end{aligned}
$$
















end
