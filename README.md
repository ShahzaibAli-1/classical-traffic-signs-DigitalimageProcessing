# Traffic Sign Classification using Classical Image Processing

## Project Overview
Complete traffic sign classification pipeline using only classical image processing techniques (no machine learning).

## Implemented Techniques

### 1. Image Filters
| Filter               | Implementation Details                      |
|----------------------|--------------------------------------------|
| Mean (3×3)           | Uniform averaging                          |
| Gaussian             | σ=1.0, separable kernel                   |
| Median               | 3×3 neighborhood median                   |
| Adaptive Median      | Dynamic window sizing (3×3 to 7×7)        |
| Unsharp Masking      | α=1.5, high-boost sharpening              |

### 2. Color Processing
- **HSV Conversion**: Manual RGB→HSV
- **Segmentation**:
  - Red: Hue [0-15]∪[165-180], S>0.4, V>0.3
  - Blue: Hue [100-130], S>0.4, V>0.3
- **Post-processing**:
  - Morphological opening/closing
  - Connected components (min_area=100)
  - Contour-based hole filling

### 3. Edge Detection (Canny)
1. Sobel gradient (manual)
2. Non-max suppression
3. Hysteresis thresholding (low=30, high=100)

### 4. Feature Extraction
| Feature          | Calculation                | Usage                      |
|------------------|----------------------------|----------------------------|
| Corner Count     | Harris detector            | Shape identification       |
| Circularity      | 4π×Area/Perimeter²        | Circle vs polygon detection|
| Aspect Ratio     | width/height               | Rectangle identification   |
| Average Hue      | HSV mean                   | Color classification       |

### 5. Rule-Based Classification
```python
if is_red and octagonal: return 14  # Stop
elif is_red and triangular: return 13  # Yield
elif is_blue and circular: return 33  # Go Right
