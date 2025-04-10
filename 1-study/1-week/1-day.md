神经网络（Neural Network）是深度学习的核心，它模仿人脑神经元的连接方式构建模型。以下是神经网络的基本组成部分的详细回顾，主要包括 **多层感知机（MLP）**、**激活函数（Activation Function）** 和 **损失函数（Loss Function）**。

---

## 一、多层感知机（MLP: Multi-Layer Perceptron）

MLP 是一种最基本的前馈神经网络（Feedforward Neural Network），通常包含：

### 1.1 网络结构

- **输入层（Input Layer）**：接收原始数据，每个输入节点对应一个特征。
- **隐藏层（Hidden Layers）**：至少一层，可能有多个。每层都由多个神经元（Neuron）组成，神经元之间全连接（Fully Connected）。
- **输出层（Output Layer）**：输出预测结果。节点个数取决于任务（回归/分类）。

### 1.2 数学表示

对于任意一层 `l`：

\[
a^{(l)} = \sigma\left(W^{(l)} a^{(l-1)} + b^{(l)}\right)
\]

- \( a^{(l-1)} \)：前一层的输出（或输入）
- \( W^{(l)} \)：第 `l` 层的权重矩阵
- \( b^{(l)} \)：偏置项（bias）
- \( \sigma \)：激活函数

其中，\( a^{(0)} = x \) 是输入特征。

---

## 二、激活函数（Activation Function）

激活函数引入非线性因素，是神经网络区别于线性模型的关键。常见的激活函数包括：

### 2.1 Sigmoid（S型函数）

\[
\sigma(x) = \frac{1}{1 + e^{-x}}
\]

- 输出范围：[0, 1]
- 缺点：
  - 梯度消失（梯度在大输入下趋近于0）
  - 输出非零均值（训练慢）

### 2.2 Tanh（双曲正切）

\[
\sigma(x) = \tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}
\]

- 输出范围：[-1, 1]
- 零均值，收敛速度比 Sigmoid 快
- 同样存在梯度消失问题

### 2.3 ReLU（Rectified Linear Unit）

\[
\sigma(x) = \max(0, x)
\]

- 非线性强、计算简单、收敛快
- 缺点：
  - Dying ReLU 问题：部分神经元在训练中输出恒为0，导致梯度无法传播

### 2.4 Leaky ReLU / Parametric ReLU

\[
\sigma(x) = \begin{cases}
x & x > 0 \\
\alpha x & x \le 0
\end{cases}
\]

- 缓解 Dying ReLU 问题，保留负梯度（例如 \(\alpha = 0.01\)）

### 2.5 Softmax（多分类输出层）

\[
\sigma(x_i) = \frac{e^{x_i}}{\sum_{j=1}^K e^{x_j}}
\]

- 常用于分类问题的输出层（多类概率）

---

## 三、损失函数（Loss Function）

损失函数度量模型输出和真实值之间的差距，训练目标就是最小化损失。

### 3.1 MSE（Mean Squared Error，均方误差）

用于回归问题：

\[
\mathcal{L}_{\text{MSE}} = \frac{1}{n} \sum_{i=1}^n (y_i - \hat{y}_i)^2
\]

- 对异常值敏感

### 3.2 MAE（Mean Absolute Error，平均绝对误差）

\[
\mathcal{L}_{\text{MAE}} = \frac{1}{n} \sum_{i=1}^n |y_i - \hat{y}_i|
\]

- 对异常值鲁棒，但不可导处梯度不连续

### 3.3 Binary Cross-Entropy（二分类交叉熵）

适用于二分类任务：

\[
\mathcal{L}_{\text{BCE}} = -\frac{1}{n} \sum_{i=1}^n \left[ y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right]
\]

- 通常搭配 Sigmoid 输出层

### 3.4 Categorical Cross-Entropy（多类交叉熵）

适用于多分类任务（one-hot 标签）：

\[
\mathcal{L}_{\text{CCE}} = -\sum_{i=1}^{n} \sum_{k=1}^{K} y_{ik} \log(\hat{y}_{ik})
\]

- 通常搭配 Softmax 输出层

---

## 四、MLP 的训练流程简述

1. **前向传播（Forward Pass）**：从输入层开始依次计算每层输出
2. **计算损失（Loss Computation）**：通过预测输出与真实标签比较
3. **反向传播（Backpropagation）**：计算损失对各层参数的梯度
4. **参数更新（Optimization）**：使用梯度下降（如SGD、Adam）更新参数

---

## 五、小结图示（简化）

```
输入 → [W, b] → 激活函数 → 隐藏层1 → ... → 激活函数 → 输出层 → 损失函数
```

- 多层线性变换 + 非线性激活 + 损失优化

---

如果你需要更深入的内容，比如反向传播公式推导、参数初始化策略、MLP 的代码实现细节，我也可以继续展开。要不要我写个 PyTorch 实现？