---
layout: post
title: Matlab中CVX工具箱使用
category: mathmodel
tags: [mathmodel]
excerpt: Matlab中CVX工具箱使用
---


# Matlab中CVX工具箱使用

CVX是一个凸优化解决工具，需要在Matlab上使用。
CVX让Matlab变成一个模型语言，可以使用Matlab的标准语法完成优化问题的求解。
## 安装
1. 下载[官方安装包](http://cvxr.com/cvx/)，解压缩到任意路径，建议和Matlab放到一起。
2. 打开Matlab，切换路径到CVX的存放路径，Matlab中运行cvx_setup命令即完成安装。

```php
cd C:\personal\cvx
cvx_setup
```

- CVX 支持的解析器`slover` 
    该版本的cvx支持4种具有不同特性的解析器`slover` :  SeDuMi、SDPT3、MOSEK 、Gurobi 
 
> 所以使用`cvx`并不需要去额外下载一个`slover`，因为CVX的安装包中已经包含了 `SeDuMi and SDPT3 `，这两个`slover`是免费许可的，默认启用的是SDPT3（The default `solver` is currently SDPT3）。

- MOSEK 包含在CVX的教育许可证和商业许可证中，使用教育邮箱申请教育版许可，即可免费使用。
- Gurobi and MOSEK 同样也可以搭载到CVX中去，但是你需要获得专业版许可证`CVX Professional license`才能使用这些功能。  
> **(可以下载带有Gurobi and MOSEK的CVX包或单独下载Gurobi and MOSEK，之后安装专业版许可证)** ，两个公司均有教育许可。

## 使用实例
1、官网实例，目标是解决如下优化问题：
$$
	\begin{array}{ll} 
	\text{minimize} & \|Ax-b\|_2 \\ 
	\text{subject to} & Cx=d \\ 
	& \|x\|_\infty\leq e 
	\end{array}
$$
在Matlab中使用以下代码即可完成优化求解，
```py
m = 20; n = 10; p = 4;
A = randn(m,n); b = randn(m,1);
C = randn(p,n); d = randn(p,1); e = rand;
cvx_begin
    variable x(n)
    minimize( norm( A * x - b, 2 ) )	%目标函数
    subject to
        C * x == d						%约束条件1
        norm( x, Inf ) <= e				%约束条件2
cvx_end	
```

2、上面的自变量是单个向量，下面给出一个多个变量的求解方案；
还是一个凸函数最优化问题，主要问题如下：
首先要把需要解决的问题写成`convex optimization`的标准问题，即明确目标函数和条件约束。
$$
\begin{array}{l}{\max _{\mathbf{g}, t}  t} \\ {\text { s.t. } \Re\left\{2 \mathbf{g}_{m-1}^{H} \mathbf{M}_{l \hat{l}} \mathbf{g}-\mathbf{g}_{m-1}^{H} \mathbf{M}_{l \hat{l}} \mathbf{g}_{m-1}^{H}\right\} \geq t, \forall l \neq \hat{l}} \\ {\quad \quad\|\mathbf{g}\|^{2} \leq M_p}\end{array}
$$
其中，$M_{l\hat{l}}$为矩阵，$M_p$为固定值，约束向量$g$的幅度。
```python
cvx_begin
    variable g(n,1) t
    maximize (t)	%目标函数
    subject to 		%约束条件
        for i = 1:56
            real(g_m'*M(i)*g - g_m'*M(i)*g_m) >= t;
        end 
        norm(g) <= M;
cvx_end
```
在Matlab中可以使用循环语句完成大量约束的枚举，更加方便。

