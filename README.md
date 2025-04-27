# Federated Multi‑Armed Bandits with Clustering (IoTAAI 2025)

本仓库实现了论文《Federated Multi‑Armed Bandits with Clustering》（IoTAAI 2025）中所提算法，针对联邦学习场景下的多臂老虎机问题，引入客户端分群（Clustering）机制以提升探索效率和通信开销的平衡。

## 📑 论文摘要

- 问题背景
  在大规模 IoT/FL 场景中，多臂老虎机（MAB）任务常分布于众多设备（客户端），直接将全局臂均值汇总中心服务器存在通信瓶颈。
- 核心贡献
  1. **分组机制**：基于各客户端的本地臂奖励分布（local_mean）使用 K‑Means 聚类，动态确定最优簇数。
  2. **分群更新**：在每个簇内进行局部训练，减少通信开销。每个簇的客户端使用相同的臂均值进行探索，避免了全局均值的计算。
- 实验结果
  – 在多种 α/β 参数组合下，实验证明分群后相比单群（全局）方法，整体 regret 明显降低，且通信次数减少。

## ⚙️ 环境与依赖

- Python 3.7+
- numpy
- matplotlib
- scikit-learn
- jupyter notebook / lab

安装示例：
```bash
pip install numpy matplotlib scikit-learn jupyter
```

## 📂 仓库结构

```
.
├── .gitignore
├── bandits.py      # PFEDUCB 主类实现
├── client.py       # client 类，实现局部/全局/混合更新
├── server.py       # server 类，实现全局统计更新
├── CPF-MAB.ipynb   # 算法主流程：探索、聚类、分组训练、结果可视化
├── test.ipynb      # 参数测试脚本：β、簇数敏感性实验
├── README.md       # 本文件
└── means/          # 均值数据集
    ├── cluster_demo_mean.npy       # 聚类示例均值数据集
    ├── distributed_means.npy       # 分布式均值数据集
    ├── movielens_norm_10_40.npy    # Movielens 数据集
    └── optimal_means.npy           # 较优结果均值数据集
```

## 🚀 快速使用

1. 克隆仓库
   ```bash
   git clone <repo_url>
   cd PF_MAB
   ```
2. 打开 `CPF-MAB.ipynb`
   - 运行前几单元，生成初始全局探索结果 `mixed_regret_0`。
   - 运行“肘部法则 + 二阶差分”单元，确定最优簇数。
   - 按分组训练并可视化最终 regret 曲线。
3. 测试脚本
   - 打开 `test.ipynb`，在不同 β、α 设置下复现实验结果。

## 🔗 主要模块

- [`PFEDUCB`](bandits.py)
- [`client`](client.py)
- [`server`](server.py)
- 聚类与数据准备逻辑见 [`CPF-MAB.ipynb`](CPF-MAB.ipynb) 与 [`test.ipynb`](test.ipynb)

## 📖 引用

若在研究中使用本代码，请引用：

> Federated Multi‑Armed Bandits with Clustering. *Proceedings of IoTAAI 2025*.

谢谢支持~