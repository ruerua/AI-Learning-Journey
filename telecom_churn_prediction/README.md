# 电信用户流失预测与特征分析系统

基于 XGBoost 的电信用户流失预测系统，实现流失风险评估与关键因素分析。

---

## 项目简介

基于电信运营商真实用户数据（7043 条 × 21 个特征），构建流失风险预测模型，主要功能包括：
- 输出用户流失概率及风险等级（高/中/低）
- 自动识别影响流失的关键因素
- 提供可视化分析报告

---

## 技术栈

| 模块 | 技术 |
|------|------|
| 数据处理 | Pandas、NumPy |
| 可视化 | Matplotlib、Seaborn |
| 机器学习 | Scikit-learn、XGBoost |
| 开发环境 | Jupyter Notebook |
| 版本管理 | Git |

---

## 核心流程

### 1. 数据清洗与特征工程
- 处理 `TotalCharges` 列类型转换与缺失值填充（中位数）
- One-Hot 编码类别特征（gender、Contract、PaymentMethod 等）
- 构造新特征：
  - `FamilySize`：伴侣 + 家属数
  - `AvgMonthlyCost`：平均月费（总消费 / (在网月数 + 1)）

### 2. 模型对比

| 模型 | 准确率 | AUC |
|------|--------|-----|
| 随机森林 | 79.49% | 0.824 |
| **XGBoost** | **80.13%** | **0.839** |

### 3. 召回率优化（针对流失类）

| 方法 | recall | precision | F1 |
|------|--------|-----------|-----|
| 原模型 | 0.532 | 0.655 | 0.587 |
| 调阈值（0.29）| 0.778 | 0.526 | 0.628 |
| 调权重（scale=2.5）| 0.781 | 0.538 | 0.637 |
| **两者结合** | **0.789** | 0.535 | **0.638** |

### 4. 关键发现
- **合约类型**是最重要的流失因素（月租型流失率是长期合约的 3 倍以上）
- 高月费、短在网时长用户流失风险显著更高

---

## 可视化示例

- 流失用户占比饼图
- 月费 / 在网时长 vs 流失箱线图
- 合约类型流失率柱状图
- 特征重要性 Top15
- 混淆矩阵

---

## 目录结构
```
AI_Learning_Journey/
├── README.md # 项目说明
├── telecom_churn_prediction/
│ ├── data/ # 原始数据（CSV，Git 忽略）
│ ├── IntoPractice/ # 实践代码
│ │ ├── 01_data_preprocessing.ipynb # 数据清洗与特征工程
│ │ └── 02_Modeling.ipynb # 建模、优化、评估
│ ├── Output/ # 可视化图表
│ └── models/ # 保存的模型文件
├── NumpyLearn/ # NumPy 学习笔记
└── PandasLearn/ # Pandas 学习笔记
```

## 运行说明
jupyter notebook
# 依次运行 telecom_churn_prediction/IntoPractice/ 下的 notebook

### 环境安装
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost

