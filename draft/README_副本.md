# ConText-CIR: Learning from Concepts in Text for Composed Image Retrieval
论文《ConText-CIR: Learning from Concepts in Text for Composed Image Retrieval》的 **PyTorch 实现**

## 环境安装

### 依赖要求
- Python 3.10 及以上
- PyTorch 2.0 及以上
- CUDA 11.8 及以上

### 安装步骤
```bash
# 安装依赖库
pip install -r requirements.txt
```

## 数据准备

### CIRR 数据集
1. 从此处下载 CIRR 数据集：[链接](https://github.com/Cuberick-Orion/CIRR)
2. 解压到 `data/cirr/` 目录

### LaSCo 数据集
1. 从此处下载：[链接](https://github.com/levymsn/LaSCo)
2. 放置到 `data/lasco/` 目录

### CIRR 重写版数据集（可选）
1. 从发布页下载重写后的标注文本
2. 放置到 `data/cirr/rewritten_captions/` 目录

### Hotel-CIR 数据集（可选）
1. 从发布页下载 Hotel-CIR 数据集
2. 解压到 `data/hotels/` 目录

---

### 配置文件
创建 `config.yaml` 配置文件：
```yaml
model_dir: ./checkpoints
cirr_data_path: ./data/cirr
hotel_data_path: ./data/hotels
lasco_data_path: ./data/lasco
```

## 模型训练

### 基础训练命令
```bash
python Train.py --datasets cirr \
                --backbone_size B \
                --train_batch_size 256 \
                --learning_rate 1e-5
```