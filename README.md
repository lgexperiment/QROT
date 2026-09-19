# QRot 复现材料入口



## 可以立即执行的核验

无需 GPU、模型权重或学生数据，只需 Python 3.10 及以上：

```sh
python3 paper_materials/qrot_manuscript_v2/submission/reproducibility/verify_results.py
```

该命令检查包内文件 SHA-256，并从 150 条补充实验逐折选模测试指标及 65 条原实验指标复算 172 个均值／样本标准差，包括两个 DKT 实验及 FA-KT 固定窗口实验。这里的“复算”不等于重新从预测算 AUC，也不等于重新训练。

安装 NumPy 后可以额外核验实际固定窗口索引函数：

```sh
python3 paper_materials/qrot_manuscript_v2/submission/reproducibility/verify_results.py --windows
```

该核验从冻结源文件提取窗口生成函数，不导入训练环境、不读取学生记录，检查短序列、长历史、单／多概念交替和窗口边界。它证明被测输入上的窗口前缀关系，不替代模型信息依赖检查。

## 数据、环境与配置

- [数据准备与来源边界](DATA.md)：官方来源、输入文件契约、处理代码入口和未恢复环节。
- [运行环境](ENVIRONMENT.md)：历史环境和固定窗口环境分别记录；CUDA 扩展需匹配本机环境。
- [重训与评估顺序](RUNBOOK.md)：准备缓存、训练、锁模、测试、汇总的真实入口。
- `data_inventory.json`：当前使用输入的路径、词表、已记录哈希及来源。数据内容未收入包。
- `experiment_index.json`：论文实验、协议、结果文件和脚本的对应。
- `fold_configs.csv`：65 个原 FA-KT 配置及 30 个固定窗口训练配置的逐折设置摘要。原配置原件也按原路径收入包。
