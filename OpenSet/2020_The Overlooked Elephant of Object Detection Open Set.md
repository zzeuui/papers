## The Overlooked Elephant of Object Detection: Open Set (2020)
WACV 2020

[[paper](https://openaccess.thecvf.com/content_WACV_2020/papers/Dhamija_The_Overlooked_Elephant_of_Object_Detection_Open_Set_WACV_2020_paper.pdf)]
[[code](https://github.com/Vastlab/Elephant-of-object-detection)]

### 💡Problem
- open-set object detection 문제를 공식화
- open-set object detection protocol를 최초로 제안
- 새로운 평가 지표를 제공
- 현재 SOTA를 달성한 object detector의 단점을 설명
- 실제 세계에서 detector를 적용하기 위한 operating point를 선택하는 것에 대한 이해 제공

### 💡Motivation  
- PASCAL VOC과 MS COCO는 closed-set과 open-set에 대한 detector의 성능을 구별할 수 있는 데이터를 제공하지 않음.
- PASCAL VOC과 MS COCO는 같은 데이터셋으로 알려지지 않은 객체를 식별할 수 있는 테스트할 수 없음.

- 데이터셋이 얼마나 open되어 있는지 openness라는 지표가 존재하지만, known과 unknown의 수만 사용하고 unknown의 빈도는 무시한다.
 
### 💡Method
1. mixed Unknown을 정의
2. openness 대신 데이터셋의 개방성을 평가할 수 있는 Wilderness Ratio 제안
3. closed-set 조건과 open-set 조건에서의 정밀도의 비율을 계산하는 Wilderness Impact 제안
    - 이상적인 검출기의 경우 closed-set 조건에서의 정밀도와 open-set 조건에서의 정밀도가 동일해야하고 WI가 0 이어야함
4. object detecor의 선택과 operating point를 선택하는 것에 대한 이해 제공

#### 1. Mixed Unknown

$K$: known object, objects of interest
- $K_{K}$: known knowns, used in training
- $K_{U}$: unknown knowns, 환경적 요인이나 왜곡으로 인해 이미 알고있는 객체의 새로운 형태로 인해 발생, used in testing

$Y$: the infinite space of labeled objects(real world)  
$U$: Y\K, unknown objects, the detector needs to reject. 알려지지 않은 모든 객체
- $U_{K} \subset U$: to ignore during training(ex: background, garbage, undesirable) 배경과 같이 데이터셋에는 존재하지만 무시되는 객체
- $U_{U} = U \backslash U_{K} = Y \backslash (K_{K} \cup K_{U} \cap U_{K})$: unknown unknown, previously unseen objects 데이터셋에도 존재하지 않는 객체

- $U_{M}$: mixed unknows, 데이터셋에는 존재하지만 배경과 달리 무시되면 안되는 객체이지만 detector가 알 수 없는 객체  
  $\Rightarrow$ detector의 성능을 저하시킴. $U_{M}$의 수를 줄여야함.

$U_{M}$의 수를 줄이기 위해 두 데이터셋을 조합함:  
데이터 셋을 조합하면, 한 데이터셋에서는 unknown으로 식별되어도
다른 데이터셋에서는 레이블링이 가능한 샘플이 있을 수 있음.
이러한 데이터셋을 mixed unknowns $U_{M}$로 정의해 이에 대해 모델이 훈련할 수 있음

PASCAL VOC 테스트셋 이미지 
\+ PASCAL VOC의 클래스가 포함되지 않는 MS COCO의 훈련셋에서 23008개의 이미지사용

#### 2. Wilderness Ratio
openness 대신 데이터셋의 개방성을 평가할 수 있는 Wilderness Ratio 제안  
<img src="https://github.com/zzeuui/papers/assets/38878047/c8d4797a-1a53-44a4-bd68-2870157a1502" width=70%\>

#### 3. Wilderness Impact
closed-set 조건과 open-set 조건에서의 정밀도의 비율을 계산하는 Wilderness Impact 제안  
<img src="https://github.com/zzeuui/papers/assets/38878047/70f4542d-c490-4629-ba3f-39038bb96dd5" width=70%\>

#### 4. Detector and operating point
- Faster RCNN is much more stable than ( RetinaNet, YOLO v2, Mask R-CNN)
- $F_{\beta}$ score
<img src="https://github.com/zzeuui/papers/assets/38878047/c966be61-c845-41ba-a758-3a23ac2a40a5" width=70%\>  

