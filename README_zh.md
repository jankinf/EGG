EGG（Emergence of lanGuage in Games）是一个用于研究多智能体游戏中离散通信的工具包。它的目标是让研究人员能够快速实现多智能体之间的通信任务，并研究在这些任务中如何自然地涌现出语言。EGG 基于 PyTorch，提供了丰富的组件和预实现的游戏，帮助研究人员探索语言涌现的机制。

---

## **EGG 的核心特性**

1. **多智能体通信**:
   - EGG 支持两个或多个智能体之间的通信任务。智能体通过离散的符号（如单词或标记）进行通信，并共同解决任务。
   - 通信方式通常不由研究人员显式定义，而是由智能体在训练过程中自行发展出“语言”。

2. **灵活的通信机制**:
   - 支持单符号或可变长度的离散通信。
   - 支持连续通信（如通过向量表示）。
   - 可以使用多种神经网络架构（如全连接网络、RNN、GRU、LSTM、Transformer 等）来实现通信。

3. **优化方法**:
   - 支持通过 **REINFORCE** 或 **Gumbel-Softmax** 优化通信通道。
   - Gumbel-Softmax 是一种允许在离散分布中进行可微采样的技巧，适用于需要反向传播的场景。

4. **简化配置**:
   - 提供了通用的组件（如检查点、优化器、TensorBoard 支持等）的简化配置。
   - 提供了一个命令行工具，支持 CUDA 加速的超参数网格搜索。

5. **预实现的游戏**:
   - EGG 提供了多个预实现的游戏，涵盖了从简单的重建任务到复杂的语言涌现任务。
   - 这些游戏可以作为研究人员的起点，帮助他们快速上手。

---

## **EGG 的结构**

EGG 的代码库结构如下：

- **`tests`**: 包含对通用组件的测试。
- **`docs`**: 包含 EGG 的文档。
- **`egg`**:
  - **`core`**: 包含通用组件，如训练器、包装器、游戏、工具等。
  - **`zoo`**: 包含预实现的游戏。
  - **`nest`**: 一个用于超参数网格搜索的工具。

---

## **EGG 的安装**

EGG 可以通过以下步骤安装：

1. **创建虚拟环境**（可选）：
   ```bash
   conda create --name egg310 python=3.10
   conda activate egg310
   ```

2. **安装 EGG**：
   - 通过 GitHub 安装：
     ```bash
     pip install git+https://github.com/facebookresearch/EGG.git
     ```
   - 或者克隆仓库并安装为可编辑模式：
     ```bash
     git clone https://github.com/facebookresearch/EGG.git
     cd EGG
     pip install --editable .
     ```

3. **运行游戏**：
   - 例如，运行 MNIST 自编码游戏：
     ```bash
     python -m egg.zoo.mnist_autoenc.train --vocab=10 --n_epochs=50
     ```

---

## **EGG 的预实现游戏**

EGG 提供了多种预实现的游戏，分为两类：

### **示例和教程游戏**
1. **MNIST 自编码教程**：
   - 一个 Jupyter Notebook 教程，逐步实现 MNIST 离散自编码器，涵盖 EGG 的基本概念。
   - 支持单符号和多符号通信，使用 REINFORCE 或 Gumbel-Softmax 优化。

2. **基础游戏**：
   - 简单的重建和判别游戏，输入来自文本文件，代码注释详细。

3. **信号游戏**：
   - 现代版的 Lewis 信号游戏，发送者看到目标图像和干扰图像，接收者根据发送者的消息选择目标图像。

4. **MNIST 自编码游戏**：
   - 发送者看到 MNIST 图像并发送一个符号，接收者尝试重建图像。

5. **求和游戏**：
   - 发送者和接收者共同训练以识别 `a^nb^n` 语法。

### **已发表的研究游戏**
1. **Channel 游戏**：
   - 研究反高效编码在涌现通信中的作用。

2. **Objects 游戏**：
   - 研究在参考游戏中如何聚焦于信息性内容。

3. **Compositionality vs Generalization 游戏**：
   - 研究涌现语言中的组合性和泛化能力。

4. **Language Bottleneck 游戏**：
   - 研究离散通信通道的信息瓶颈特性。

---

## **EGG 的使用场景**

1. **语言涌现研究**：
   - 通过多智能体通信任务，研究语言如何自然地涌现。
   - 例如，研究智能体如何在没有显式指导的情况下发展出有效的通信协议。

2. **自编码器和风格迁移**：
   - 使用 EGG 实现自编码器任务，研究离散通信通道在信息压缩中的作用。
   - 例如，MNIST 风格迁移任务。

3. **组合性和泛化能力研究**：
   - 研究智能体在复杂任务中的组合性和泛化能力。

---

## **EGG 的引用**

如果 EGG 对你的研究有帮助，请引用以下文献：
```bibtex
@misc{kharitonov:etal:2021,
  author = "Kharitonov, Eugene and Dess{\`i}, Roberto and Chaabouni, Rahma and Bouchacourt, Diane and Baroni, Marco",
  title = "{EGG}: a toolkit for research on {E}mergence of lan{G}uage in {G}ames",
  howpublished = {\url{https://github.com/facebookresearch/EGG}},
  year = {2021}
}
```

---

## **EGG 的贡献和测试**

- **贡献**：请阅读贡献指南 [here](.github/CONTRIBUTING.md)。
- **测试**：运行 `pytest` 以确保所有测试通过：
  ```bash
  python -m pytest
  ```

---

## **总结**

EGG 是一个强大的工具包，适用于研究多智能体通信和语言涌现。它提供了丰富的预实现游戏和灵活的组件，帮助研究人员快速上手并探索复杂的研究问题。无论是初学者还是经验丰富的研究人员，都可以通过 EGG 实现自己的通信任务并研究语言涌现的机制。