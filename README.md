# 🧠 Brain Tumor Detection from MRI Scans

![Python](https://img.shields.io/badge/Python-3.x-blue.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-FF6F00.svg?logo=tensorflow)
![OpenCV](https://img.shields.io/badge/OpenCV-4.x-5C3EE8.svg?logo=opencv)
![License](https://img.shields.io/badge/License-MIT-green.svg)

> An End-to-End Deep Learning and Computer Vision pipeline designed to automatically classify MRI scans and assist healthcare professionals in diagnosing brain tumors.

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/5/5f/Hirnmetastase_MRT-T1_KM.jpg" alt="Brain MRI Banner" width="600"/>
</p>

---

## 📑 Table of Contents
1. [Project Overview & Objectives](#1-project-overview--objectives)
2. [What is a Brain Tumor?](#2-what-is-a-brain-tumor)
3. [The Dataset](#3-the-dataset)
4. [Pipeline & Preprocessing](#4-pipeline--preprocessing)
5. [Model Architecture](#5-model-architecture)
6. [Results & Evaluation](#6-results--evaluation)
7. [Installation & Requirements](#7-installation--requirements)

---

## 🎯 1. Project Overview & Objectives

The main purpose of this project is to build a robust Convolutional Neural Network (CNN) model that classifies whether a subject has a tumor based on an MRI scan. 

This is a binary classification problem:
* `NO` - No tumor, encoded as `0`
* `YES` - Tumor present, encoded as `1`

I used `accuracy` as the primary metric to justify the model's performance, which is defined as:

$$\text{Accuracy} = \frac{\text{Number of correctly predicted images}}{\text{Total number of tested images}} \times 100\%$$

## 🧠 2. What is a Brain Tumor?

> A brain tumor occurs when abnormal cells form within the brain. There are two main types of tumors: cancerous (malignant) tumors and benign tumors. Cancerous tumors can be divided into primary tumors, which start within the brain, and secondary tumors, which have spread from elsewhere, known as brain metastasis tumors. 
> 
> Symptoms may include headaches (classically worse in the morning), seizures, vision problems, vomiting, and mental changes. As the disease progresses, unconsciousness may occur.
> 
> *Source: [Wikipedia](https://en.wikipedia.org/wiki/Brain_tumor)*

## 📂 3. The Dataset

The image data used for this problem is the [Brain MRI Images for Brain Tumor Detection](https://www.kaggle.com/navoneel/brain-mri-images-for-brain-tumor-detection) from Kaggle. 

<p align="center">
  <img src="https://via.placeholder.com/600x250.png?text=Placeholder:+Raw+MRI+Scans+(YES/NO)" alt="Raw Data Samples" />
</p>

## ⚙️ 4. Pipeline & Preprocessing

Medical images require careful preprocessing to ensure the model learns physiological features rather than background noise. 

1. **Extreme Point Cropping:** An automated contour detection algorithm using OpenCV that crops out the unnecessary black background, allowing the CNN to focus exclusively on the brain anatomy.
2. **CLAHE (Contrast Limited Adaptive Histogram Equalization):** Applied to enhance the contrast of the MRI scans, highlighting fine tissue details.
3. **Data Augmentation:** Applied dynamic rotations, zooms, and flips to prevent overfitting and improve generalization.

<p align="center">
  <img src="https://via.placeholder.com/600x300.png?text=Placeholder:+Before+and+After+Preprocessing" alt="Preprocessing Steps" />
</p>

## 🏗️ 5. Model Architecture

I initially experimented with the **VGG-16** model architecture to establish a baseline. To optimize parameter efficiency and push the accuracy higher, the final pipeline was transitioned to **EfficientNetB3** using Transfer Learning.

* **Callbacks Used:** `EarlyStopping` (to prevent overfitting) and `ReduceLROnPlateau` (to dynamically adjust the learning rate).

## 📊 6. Results & Evaluation

The model achieved strong results, proving its potential as a medical triage tool.

| Set | Accuracy |
|:-:|:-:|
| **Validation Set** | ~88% |
| **Test Set** | ~80% |

*(Note: The validation set was used during training to tune hyperparameters, while the test set was kept completely unseen for final evaluation).*

### Confusion Matrix & Training History
<p align="center">
  <img src="https://via.placeholder.com/400x300.png?text=Placeholder:+Accuracy/Loss+Graphs" alt="Training Graphs" width="45%"/> 
  &nbsp;
  <img src="https://via.placeholder.com/400x300.png?text=Placeholder:+Confusion+Matrix" alt="Confusion Matrix" width="45%"/>
</p>

**Current Limitation:** The dataset used is relatively small. The statistical variance in the test set is high, meaning a larger, clinical-grade dataset is required for real-world medical deployment.

## 💻 7. Installation & Requirements

To replicate this project on your local machine, follow these steps:

**1. Clone the repository:**
```bash
git clone [https://github.com/a7med-830/brain-tumor-detection.git](https://github.com/a7med-830/brain-tumor-detection.git)
cd brain-tumor-detection
