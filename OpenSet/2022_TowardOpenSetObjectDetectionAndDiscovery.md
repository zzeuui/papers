## Towards Open-Set Object Detection and Discovery (2022)
[blog](https://blog.naver.com/yoon_03_28/223318043693)

### 💡Problem
propose a framework to detect known objects
and discover novel visual categories for unknown objects without human effort
named Open-Set Object Detection and Discovery(OSODD).

### 💡Motivation  
Open-set object detection(OSOD)
- all the predicted unknown object share the same category as "unknown"
- require incremental learning via a human-in-the-loop approach to label novel classes

### 💡Method
Add memory buffer and OCD part

#### ODR
- Contrastive Clustering: To learn more discriminative representation for each class
- memory buffer: save known and unknown information for OCD

#### OCD
-  Representation Learning:  
    -  class-agnostic augmentation: generalize feature
    -  contrastive learning: To learn more discriminative feature for instance
-  Category Number Estimation & Novel Category Labelling: K-means + K-mean++
  
<img src="https://github.com/zzeuui/papers/assets/38878047/a167e64f-c884-45e4-9c1f-f413ec4a7c86" width="70%"/>

### 💡Experiment
#### Dataset
- Pascal VOC 2007
- MS-COCO

#### Evaluation Metrics
- Object Detection Metrics
  - mean Average Precision(mAP)
  - UDR(Unknown Detection Recall)
  - UDP(Unknown Detection Precision)
- Category Discovery Metrics
  - ACC
  - NMI
  - Purity
