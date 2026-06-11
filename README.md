# Nailong Detector

> 基于 YOLOv8 的奶龙目标检测项目

![YOLOv8](https://img.shields.io/badge/YOLOv8-SOTA-blue)
![Python](https://img.shields.io/badge/Python-3.8%2B-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 项目简介

**Nailong Detector** 是一个基于 **YOLOv8** 训练的目标检测项目，用于识别和检测图片或视频中的 **“奶龙”** 形象。

本项目包含完整的目标检测流程，包括：

- 数据清洗
- 视频抽帧
- 模型训练
- 模型推理
- 结果可视化

## 项目结构

```text
Nailong-YOLO-Project/
├── weights/
│   └── best.pt              # 训练好的最佳模型权重
├── assets/
│   └── demo.jpg             # 演示图片
├── data.yaml                # 数据集配置文件
├── classes.txt              # 类别名称文件
├── train.py                 # 模型训练脚本
├── clean_data.py            # 数据清洗脚本
├── extract_frames.py        # 视频抽帧脚本
├── requirements.txt         # 项目依赖文件
└── README.md                # 项目说明文档
```

## 环境安装

本项目建议使用 **Python 3.8+**。

### 1. 克隆项目

```bash
git clone https://github.com/你的用户名/Nailong-YOLO-Project.git
cd Nailong-YOLO-Project
```

### 2. 安装依赖

```bash
pip install -r requirements.txt
```

核心依赖包括：

- ultralytics
- opencv-python
- moviepy
- torch

## 快速开始

### 1. 命令行推理

使用项目提供的预训练权重 `weights/best.pt` 进行目标检测。

#### 检测图片

```bash
yolo detect predict model=weights/best.pt source="path/to/your/image.jpg" show=True
```

#### 检测视频

```bash
yolo detect predict model=weights/best.pt source="path/to/your/video.mp4" show=True
```

检测结果默认保存到：

```text
runs/detect/predict/
```

### 2. Python 脚本推理

```python
from ultralytics import YOLO

# 加载模型
model = YOLO("weights/best.pt")

# 执行预测
results = model("test.jpg", show=True, save=True)
```

## 模型训练

如果需要重新训练模型，请先确保 `data.yaml` 中的数据集路径配置正确。

运行训练脚本：

```bash
python train.py
```

也可以直接使用 YOLOv8 命令训练：

```bash
yolo detect train model=yolov8n.pt data=data.yaml epochs=100 imgsz=640
```

## 工具脚本说明

### extract_frames.py

用于从视频中按固定间隔抽取图片帧，便于制作目标检测数据集。

运行方式：

```bash
python extract_frames.py
```

### clean_data.py

用于清洗数据集，例如：

- 删除损坏图片
- 删除没有对应标签的图片
- 删除无效标注文件

运行方式：

```bash
python clean_data.py
```

## 模型信息

| 项目 | 说明 |
|---|---|
| 模型架构 | YOLOv8 |
| 训练框架 | PyTorch |
| 检测类别 | nailong |
| 权重文件 | weights/best.pt |
| 类别文件 | classes.txt |

## 数据集配置示例

`data.yaml` 示例：

```yaml
path: ./dataset
train: images/train
val: images/val

names:
  0: nailong
```

请根据自己的数据集路径进行修改。

## 贡献

欢迎提交 Issue 或 Pull Request 来改进本项目。

可以贡献的内容包括：

- 改进数据集
- 优化训练参数
- 提升检测精度
- 修复脚本问题
- 补充文档说明

## License

本项目基于 MIT License 开源。
