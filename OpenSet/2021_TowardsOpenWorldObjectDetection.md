## Towards Open World Object Detection (2021)
[blog](https://blog.naver.com/yoon_03_28/223316864776)

### 💡Problem
‘Open World Object Detection’
1) identify objects that have not been introduced to it as ‘unknown’, without explicit supervision to do so, and
2) incrementally learn these identified unknown categories without forgetting previously learned classes,
when the corresponding labels are progressively received. 

### 💡Motivation  
Open-set Learning + Incremental Learning + Detection

<img src="https://github.com/zzeuui/papers/assets/38878047/b1f982b3-8177-416b-b52b-fa994066d441" width="50%"/>

### 💡Method
- Faster RCNN: detect interest region, auto-labelling unknowns with RPN
- Contrastive Clustering: To learn more discriminative representation for each class
- Energy based unknown identifier: estimates the compatibility between observed variables feature and possible set of output variables labels using a single output scalar.
- Alleviating Forgetting: for Incremental Learning
 
<img src="https://github.com/zzeuui/papers/assets/38878047/40bed31e-726f-4380-bb93-43c1a08bd484" width="50%"/>

### 💡Experiment
#### Dataset
- Pascal VOC 2007
- MS-COCO

#### Evaluation Metrics
- Wilderness Impact (WI)
- Absolute Open-Set Error (A-OSE)
- mean Average Precision(mAP)
