

# Exploring Feature Pyramid Networks for Object Detection on PASCAL VOC

[Full Report](https://drive.google.com/file/d/15yTOebQcrX_n-U9fAkb6eqjYIHO8McLI/view?usp=sharing)

---

## Overview
This study evaluates **Feature Pyramid Networks (FPN)** for object detection under constrained budgets using a **20% subset of PASCAL VOC 2012**. We compare:

1. Faster R-CNN (no FPN)
2. Faster R-CNN + FPN
3. Improved FPN with multi-scale augmentation and light random cropping

---

## Dataset & Setup
- **Dataset**: PASCAL VOC 2012 (20% train subset)
- **Backbone**: ResNet-50
- **Training**: Short schedules (2 epochs), batch size 4, AMP enabled
- **Evaluation Metrics**: mAP@0.5, AP stratified by object size (small/medium/large)

---

## Key Results
| Model           | mAP  | AP_small | AP_medium | AP_large |
|-----------------|------|----------|-----------|----------|
| noFPN           | 0.0002 | 0.0000 | 0.0000   | 0.0003   |
| FPN             | 0.2926 | 0.0053 | 0.1126   | 0.2771   |
| Improved FPN    | 0.7192 | 0.0826 | 0.1977   | 0.6586   |

**Observations**:  
- FPN significantly improves performance, especially on medium/large objects.  
- Stronger augmentation and cropping further boost mAP.  
- Small-object AP remains challenging due to limited resolution.

---

## Practical Takeaways
- FPN is highly effective even under tight compute budgets.  
- Multi-scale jitter + light cropping + box sanitization stabilizes training and improves results.  
- Always report size-stratified metrics to understand performance across object scales.

---

## Reproducibility
- Seed: 42  
- Framework: PyTorch + Torchvision  
- Short schedules and limited GPU memory (Kaggle free GPU)  
- Data transforms: Random horizontal flip, FixedResize or multi-scale jitter  
- Losses: Faster R-CNN RPN + ROI classification & regression
