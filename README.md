# 🧠 YOLOv3 Object Detection & Bounding Box Evaluation

This repository implements a complete **object detection and evaluation pipeline** using **YOLOv3**, including:

- A modified YOLOv3 model with **skip connections**  
- Decoding and post-processing of network outputs  
- XML-based extraction of ground truth bounding boxes  
- IOU-based evaluation and mean Average Precision (mAP) computation  
- Visual comparisons between predictions and ground truth

All documentation and methodology are based on the project report included in this repository. :contentReference[oaicite:1]{index=1}

---

## 🚀 Project Overview

This project enhances YOLOv3 by integrating additional **encoder–decoder skip connections**, improving the recovery of fine spatial details during upsampling. Feature maps from encoder layers are concatenated with decoder layers of matching spatial resolution, allowing the model to reconstruct more precise object boundaries. :contentReference[oaicite:2]{index=2}

The workflow includes:

- Loading YOLOv3 and customizing the architecture
- Preprocessing images for object detection
- Decoding predictions (anchors, confidence scores, NMS)
- Extracting ground-truth bounding boxes from XML metadata
- Computing evaluation metrics across multiple IoU thresholds
- Visualizing predicted vs. real bounding boxes

---

## 🧩 Model Architecture

### 🔗 Skip Connections
Six skip connections are added between encoder and decoder layers:

- Each decoder layer receives feature maps from the corresponding encoder layer  
- Concatenation restores spatial detail lost during downsampling  
- Decoder layers produce sharper, more accurate bounding boxes

> This significantly helps the decoder reconstruct fine details and shapes.  
> Documented in the project report. :contentReference[oaicite:3]{index=3}

---

## 🗂 Dataset & Ground Truth Extraction

Ground truth bounding boxes are obtained from **XML files** included with the dataset.

Pipeline:

1. Parse XML files  
2. Extract bounding box coordinates  
3. Align them with corresponding images  
4. Prepare (image, ground truth) pairs for evaluation

The repository provides a function for clean extraction of bounding box coordinates.  
Examples and resulting plots appear in the report. :contentReference[oaicite:4]{index=4}

---

## 🔍 Object Detection Process

The detection pipeline includes:

- Setting input size (416×416)
- Loading and preparing an image
- inferring predictions using `yolov3.predict`
- Decoding raw outputs:
  - anchor selection  
  - confidence filtering  
  - non-max suppression (NMS)
- Rendering final bounding boxes onto the original image

This produces visual overlays of detected objects with confidence scores. :contentReference[oaicite:5]{index=5}

---

## 📊 Evaluation (IoU & mAP)

With both predicted and ground-truth boxes available, the project computes:

- Intersection over Union (IoU)  
- Mean Average Precision (mAP) across multiple IoU thresholds  

Although the final numerical mAP values were not perfect, the evaluation logic is structured correctly and very close to a full implementation. :contentReference[oaicite:6]{index=6}

---
