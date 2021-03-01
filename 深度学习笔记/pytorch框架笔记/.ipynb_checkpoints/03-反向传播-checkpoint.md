# 反向传播

## 回顾

线性模型：$\hat y=x*w$，其中$w$为权重，$x$为输入数据。

![image-20210123164445655](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123164445655.png)

随机梯度下降：
$$
w=w-\alpha\frac{\partial loss}{\partial w}
$$
其中，
$$
\frac{\partial loss_n}{\partial w} = 2\cdot x_n\cdot (x_n\cdot w-y_n)
$$
对于复杂模型，考虑如何计算梯度？

![image-20210123164725244](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123164725244.png)

## 计算图

一个两层的神经网络：
$$
\hat y = W_2(W_1\cdot X+b_1)+b_2
$$
![image-20210123165318495](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123165318495.png)

其中，$W_1$与$X$通过矩阵乘法得到隐藏层$H^{(1)}$。

![image-20210123165645694](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123165645694.png)

$H^{(1)}$和$b_1$通过加法运算得到新的一个$X$。

![image-20210123165811774](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123165811774.png)

神经网络的第一层，就这样计算完毕了，神经网络的第二层和运行过程和第一层一样。

![image-20210123170028670](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123170028670.png)

## 关于两层神经网络的问题

将各个层的计算过程进行统一，可以得到如下模型：

![image-20210123171030329](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123171030329.png)

如上可知，无论神经网络有多少层，都是线性的，实际只是做了一层计算。

于是为了解决这个问题，加一个非线性的激活函数，比如$sigmoid$函数，在每个线性模型后得到的线性数据，进行非线性变换。

![image-20210123171703072](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123171703072.png)

## 函数的复合和链式法则

> 矩阵书籍：[地址](https://www.math.uwaterloo.ca/~hwolkowi/matrixcookbook.pdf)

![image-20210123172254736](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123172254736.png)
$$
\frac{\partial f(g(x))}{\partial x} = \frac{\partial f(g(x))}{\partial g(x)}\cdot \frac{\partial g(x)}{\partial x}
$$

1. 创建计算图$(Forward)$

![image-20210123172738099](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123172738099.png)

2. 局部梯度

![image-20210123190454655](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123190454655.png)

3. 给定连续节点的梯度

![image-20210123212343416](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123212343416.png)

4. 用链式法则计算梯度

![image-20210123212422203](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123212422203.png)

![image-20210123212941634](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123212941634.png)

**Example：$f=x\cdot w，x=w，w=3$**

* **forward**

![image-20210123213010427](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123213010427.png)

* **backward**

![image-20210123213058446](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123213058446.png)

![image-20210123213417842](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123213417842.png)

![image-20210123213515866](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123213515866.png)

  

## 线性模型的计算图

![image-20210123214445592](assets/03-%E5%8F%8D%E5%90%91%E4%BC%A0%E6%92%AD/image-20210123214445592.png)

其中，残差项$r=\hat y-y$

