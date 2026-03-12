# LiDAR Segmentation using Segment Anything Model (SAM)

## Research Paper
This repository contains the implementation for the research work:

**Efficient Segmentation and Analysis Automation of LiDAR Data**

Authors: 

Shreya Vijaykumar Upadhye 

Sweekruti S Nayak  
Tejawsini Mullalli   
P.G Sunitha Hiremath  
Sujay Raghavendra  

KLE Technological University, Hubballi, India

Presented at:  
**8th International Conference on Recent Trends in Image Processing & Pattern Recognition (RTIP2R 2025)**

---

# Overview

LiDAR (Light Detection and Ranging) sensors generate dense **3D point clouds** that represent real-world environments. However, these point clouds are **large, complex, and unstructured**, making segmentation and analysis difficult.

This project introduces an **automated pipeline** that:

- Converts **3D LiDAR point clouds → 2D cylindrical projection images**
- Performs **segmentation using the Segment Anything Model (SAM)**
- Maps segmentation masks **back into the original 3D point cloud**

This approach simplifies LiDAR data interpretation while maintaining spatial accuracy.

---

# Applications

The system can be used in multiple real-world domains:

- Autonomous Driving
- Urban Planning
- Environmental Monitoring
- Smart City Development
- Disaster Management

LiDAR segmentation helps identify objects such as:

- Roads
- Buildings
- Vegetation
- Urban structures

---

# Dataset

The project uses the **KITTI Velodyne LiDAR dataset**.

Dataset features:

- High-resolution 3D point clouds
- Velodyne HDL-64E LiDAR sensor
- Real-world urban and rural scenes
- Annotated ground truth for evaluation

Each LiDAR point contains:

```
(X, Y, Z, Reflectance)
```

Stored in:

```
.bin binary files
```

Dataset size: **26.5 GB**

---

# Methodology

The system follows a **modular processing pipeline**.

## 1. Data Preprocessing

- Load LiDAR `.bin` files
- Extract point coordinates (X, Y, Z) and reflectance
- Filter noise and unnecessary ground points

---

## 2. 3D → 2D Cylindrical Projection

3D point clouds are converted into structured **2D projection images**.

The projection uses:

- Azimuth angle (horizontal)
- Elevation angle (vertical)

Benefits:

- Reduces computational complexity
- Enables use of image segmentation models

---

## 3. HSV Enhancement

To improve feature visibility:

- 2D projection image converted to **HSV color space**
- Enhances edges and depth differences
- Highlights structural boundaries

Since SAM requires RGB input:

```
HSV → RGB conversion
```

is performed before segmentation.

---

## 4. Segmentation using SAM

The **Segment Anything Model (SAM)** with **ViT-H backbone** is used.

SAM automatically:

- Detects visual patterns
- Separates object regions
- Generates pixel-accurate segmentation masks

Objects detected include:

- Roads
- Buildings
- Vegetation
- Surrounding structures

---

## 5. Mapping Segmentation Back to 3D

The segmented 2D masks are projected back to the original **3D point cloud**.

Process:

- Each pixel corresponds to original LiDAR points
- Labels assigned to those points
- Spatial structure preserved

Final output:

```
Segmented 3D point cloud (.ply file)
```

---

# Results

The system successfully processes LiDAR data and produces accurate segmentation.

Key observations:

- Clear 2D projection from raw LiDAR data
- Accurate segmentation masks using SAM
- Efficient mapping back to 3D space

Performance comparison:

| Model | mIoU | Road IoU | Building IoU | Runtime |
|------|------|------|------|------|
| SAM (Proposed) | 58.4 | 71.2 | 66.5 | 5 FPS |
| PointNet++ | 63.2 | 74.0 | 68.1 | 3 FPS |

SAM provides **competitive accuracy with faster runtime**, making it efficient for large-scale LiDAR analysis.

---

# Project Structure

```
lidar-segmentation-sam
│
├── Mini_code.ipynb
├── requirements.txt
├── README.md
```

---

# Installation

Clone the repository:

```bash
git clone https://github.com/ShreyaUpadhye7/lidar-segmentation-sam.git
cd lidar-segmentation-sam
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# Running the Project

Open the notebook:

```
Mini_code.ipynb
```

The notebook performs:

1. Load LiDAR `.bin` data  
2. Convert 3D point cloud to 2D cylindrical image  
3. Enhance image using HSV transformation  
4. Apply SAM segmentation  
5. Map results back to 3D point cloud  

---

# Future Work

Future improvements may include:

- Real-time LiDAR segmentation
- Multimodal fusion (RGB + LiDAR)
- Lightweight SAM variants
- Hardware acceleration for autonomous vehicles

---

# Author

**Shreya Vijaykumar Upadhye**

Computer Science Engineering  
KLE Technological University, India

Research Interests:

- Computer Vision
- LiDAR Processing
- Deep Learning
- Autonomous Systems

---

# Citation

If you use this work, please cite:

```
Upadhye, S. V., Nayak, S. S., Mullalli, T., Hiremath, P. G. S., & Raghavendra, S.
Efficient Segmentation and Analysis Automation of LiDAR Data.
RTIP2R 2025.
```

