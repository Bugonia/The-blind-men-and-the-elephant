# Lipschitz 常数小为什么允许更大的学习率

在梯度下降中，我们考虑目标函数 \(f(x)\)，更新规则为

\[
x_{t+1}=x_t-\eta \nabla f(x_t),
\]

其中 \(\eta\) 是学习率。

如果 \(f\) 的梯度是 \(L\)-Lipschitz 连续的，即

\[
\|\nabla f(x)-\nabla f(y)\|\le L\|x-y\|,
\]

那么 \(f\) 是 \(L\)-smooth 函数，并满足下降引理：

\[
f(y)\le f(x)+\nabla f(x)^\top (y-x)+\frac{L}{2}\|y-x\|^2.
\]

令

\[
y=x-\eta \nabla f(x),
\]

代入下降引理：

\[
f(x-\eta \nabla f(x))
\le
f(x)+\nabla f(x)^\top(-\eta \nabla f(x))
+\frac{L}{2}\|-\eta \nabla f(x)\|^2.
\]

化简可得：

\[
f(x-\eta \nabla f(x))
\le
f(x)-\eta\|\nabla f(x)\|^2
+\frac{L\eta^2}{2}\|\nabla f(x)\|^2.
\]

进一步合并：

\[
f(x-\eta \nabla f(x))
\le
f(x)
-\eta\left(1-\frac{L\eta}{2}\right)\|\nabla f(x)\|^2.
\]

为了保证每一步目标函数下降，需要下降项为正，即

\[
\eta\left(1-\frac{L\eta}{2}\right)>0.
\]

由于 \(\eta>0\)，因此需要

\[
1-\frac{L\eta}{2}>0,
\]

也就是

\[
\eta<\frac{2}{L}.
\]

因此，允许的最大学习率与 Lipschitz 常数 \(L\) 成反比：

\[
\eta_{\max}\propto \frac{1}{L}.
\]

这说明：**Lipschitz 常数越小，梯度变化越平缓，梯度下降中允许选择的学习率越大；Lipschitz 常数越大，梯度变化越剧烈，学习率必须更小，否则优化过程容易震荡或发散。**

在实际深度学习训练中，常见的保守选择是

\[
0<\eta\le \frac{1}{L},
\]

因为这样不仅能保证下降，而且下降量有更清晰的下界：

\[
f(x-\eta\nabla f(x))
\le
f(x)-\frac{\eta}{2}\|\nabla f(x)\|^2.
\]
