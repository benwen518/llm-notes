# 神经网络基本组成

## 一、多层感知机（MLP）

一个多层感知机的每一层满足如下公式：

$$
a^{(l)} = \sigma\left(W^{(l)} a^{(l-1)} + b^{(l)}\right)
$$

其中：

- $a^{(0)} = x$ 表示输入
- $W^{(l)}$：第 $l$ 层权重矩阵
- $b^{(l)}$：偏置项
- $\sigma$：激活函数

---

## 二、激活函数

### 1. Sigmoid

$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$

输出范围 $[0, 1]$，容易产生梯度消失问题。

### 2. Tanh

$$
\sigma(x) = \tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}
$$

输出范围 $[-1, 1]$。

### 3. ReLU

$$
\sigma(x) = \max(0, x)
$$

### 4. Leaky ReLU

$$
\sigma(x) = \begin{cases}
x & x > 0 \\\\
\alpha x & x \le 0
\end{cases}
$$

---

## 三、损失函数

### 1. 均方误差 MSE

$$
\mathcal{L}_{\text{MSE}} = \frac{1}{n} \sum_{i=1}^n (y_i - \hat{y}_i)^2
$$

### 2. 交叉熵损失（Binary Cross Entropy）

$$
\mathcal{L}_{\text{BCE}} = -\frac{1}{n} \sum_{i=1}^n \left[ y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right]
$$

### 3. 多分类交叉熵（Categorical Cross Entropy）

$$
\mathcal{L}_{\text{CCE}} = -\sum_{i=1}^{n} \sum_{k=1}^{K} y_{ik} \log(\hat{y}_{ik})
$$

---

## 四、训练流程

