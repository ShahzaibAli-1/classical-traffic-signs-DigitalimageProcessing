# 🚦 Traffic Sign Classification using Classical Image Processing

Welcome to a full traffic sign classification pipeline designed **entirely using classical image processing** techniques — no machine learning, no neural networks! 🤖🤞

---

## 📚 Table of Contents

1. [📌 Project Overview](#-project-overview)
2. [🧪 Implemented Techniques](#-implemented-techniques)

   * [🗈️ Image Filters](#%ef%b8%8f-image-filters)
   * [🎨 Color Space Conversion & Segmentation](#-color-space-conversion--segmentation)
   * [🪞 Edge Detection (Canny)](#-edge-detection-canny)
   * [📊 Feature Extraction](#-feature-extraction)
   * [📋 Rule-Based Classification](#-rule-based-classification)
   * [🧽 Geometric Normalization](#-geometric-normalization)
3. [👨‍💻 Contributors](#-contributors)

---

## 📌 Project Overview

This project focuses on detecting and classifying traffic signs using **only classical computer vision techniques**, demonstrating that deep learning is not always necessary for robust image analysis.

📸 **Input**: Raw RGB images of traffic signs
🎯 **Output**: Predicted traffic sign class IDs (based on handcrafted rules)

---

## 🧪 Implemented Techniques

### 🗈️ Image Filters

| Filter Type         | Description                               |
| ------------------- | ----------------------------------------- |
| `Mean Filter (3×3)` | Applies uniform averaging (box blur)      |
| `Gaussian Filter`   | Separable kernel, σ=1.0 or configurable   |
| `Median Filter`     | Replaces with neighborhood median (3×3)   |
| `Adaptive Median`   | Window size dynamically grows to 7×7      |
| `High-Boost Filter` | Sharpens using: I + k(I - Blurred), k=1.5 |

✨ These help remove noise, sharpen features, and enhance edges.

---

### 🎨 Color Space Conversion & Segmentation

#### ✅ Manual RGB to HSV Conversion

Custom implementation based on color channel relationships.

#### 🌟 Color Segmentation

| Color | Hue Range            | Saturation | Value |
| ----- | -------------------- | ---------- | ----- |
| Red   | \[0–15] ∪ \[345–360] | > 0.4      | > 0.3 |
| Blue  | \[100–130]           | > 0.4      | > 0.3 |

#### 🧹 Post-Processing

* Noise removal using neighborhood logic
* Removes isolated pixels (similar to morphological opening)
* Ensures only meaningful sign shapes are preserved ✅

---

### 🪞 Edge Detection (Canny - Manual)

1. **Gaussian Blur** (pre-smoothing)
2. **Sobel Filter** (gradient magnitude and direction)
3. **Non-Maximum Suppression** (thin edges)
4. **Hysteresis Thresholding** (retain strong & connected weak edges)

📏 Parameters:

* Low Threshold = 50
* High Threshold = 100
* Sigma = 1.0

---

### 📊 Feature Extraction

| Feature      | Purpose                    | Method                                       |
| ------------ | -------------------------- | -------------------------------------------- |
| Corner Count | Detect polygonal shapes    | Harris detector (optional)                   |
| Circularity  | Detect circles vs polygons | $4π \times \text{Area} / \text{Perimeter}^2$ |
| Aspect Ratio | Detect rectangular shapes  | Width ÷ Height                               |
| Average Hue  | Dominant color detection   | Mean Hue of segmented region                 |

These help build a **rule-based logic** for classifying sign types.

---

### 📋 Rule-Based Classification

Custom rules based on geometric and color features:

```python
if is_red and octagonal:
    return 14  # Stop 🛘
elif is_red and triangular:
    return 13  # Yield ⚠️
elif is_blue and circular:
    return 33  # Mandatory: Turn Right ➡️
```

🔧 You can expand this logic to include more classes and shape variations.

---

### 🧽 Geometric Normalization

Ensures signs are **aligned**, **scaled**, and **centered**:

* ✅ Affine Transformation: Combines rotation, scaling, translation
* 📊 Perspective Correction: Handles tilted or slanted views
* 📆 Output size: Normalized to (200×200 px)

Helps ensure consistency in feature extraction & classification.

---

## 👨‍💻 Contributors

A big shout-out to the amazing team behind this project! 🙌

| Name               | GitHub Profile                                         |
| ------------------ | ------------------------------------------------------ |
| 🧠 Abdullah Naeem | [@Abdullah Naeem](https://github.com/abdullah-naeem600) |
| ⚙️ Ammar Ahmed  | [@Ammar Ahmed](https://github.com/i220514-AmmarAhmed)       |
| 🎨 Muhammad Umar   | [@Muhammad Umar](https://github.com/Kaizer321)     |

> 🔁 Feel free to fork, contribute, or suggest new rules and filters!

---

## 🌟 Final Notes

This project demonstrates that **pure image processing** still has a place in modern CV pipelines, especially for problems like sign recognition, where structure and color are distinct.

---

🌟 Star the repo if you liked the project!
📩 For suggestions or bugs, feel free to open an issue.
