## UC-OWOD: Unknown-Classified Open World Object Detection (2022)
ECCV2022  
[[paper](https://www.ecva.net/papers/eccv_2022/papers_ECCV/papers/136700191.pdf)]
[[code](https://github.com/JohnWuzh/UC-OWOD)]

### 💡Problem
- Unknown-Classified Open World Object Detection (UC-OWOD) 문제를 정식화
  - UC-OWOD는 unknown object를 감지하고 unknown이라도 서로 다른 객체일 경우 서로 다른 클래스로 분류하는 것을 목표로 함.
- UC-OWOD를 해결할 수 있는 two-stage object detector를 제안. 
- UC-OWOD 문제를 정확하게 평가하기 위해 unknown object의 classification 및 localization 성능을 파악하하는 새로운 metric을 제안

### 💡Motivation
- 기존 작업은 unknown만 구별하고, unknown 사이의 차이를 식별하지 못 함.
- 기존의 평가 방법은 known과 unknown을 식별하는지만 파악할 수 있음. 서로 다른 unknown object가 동일한 클래스로 감지되는 상황을 평가할 수 없음

### 💡Method
1. unknown label-aware proposal (ULP)/unknown-discriminative classification head (UCH): 배경으로부터 unknown object 발견
RPN으로 관심 지역 예측하고, NMS로 중복 제거. objectness score를 기준으로 상위 k개의 예측을 추림. 그리고 배경을 제외하기 위해서 objectness score가 임계값보다 크면 unknown으로 지정함.

2. similarity-based unknown classification (SUC): unknown object를 구별
clustering으로 unknown 사이의 차별점을 구별함. pairwise classification을 채택해서 두 샘플이 유사한지 similarity를 계산해서 구별. 이때 샘플 쌍은 known-known, unknown-known, known-background, unknown-background 중 하나임. similarity가 임계값 a보다 크면 positive로, 임계값보다 b보다 작으면 negative로, 아니면 무시함.

3. unknown clustering refinement (UCR): unknown object를 classification & 알고리즘 견고성 향상
unknown object의 임베딩 E와 클러스터의 중심 O를 얻고, Student's t-distribution분포를 사용해 E와 O 사이의 soft assignment를 계산함.

### 💡Experiments
서로 다른 unknown을 위한 정확한 레이블이 없어 mAP를 계산할 수 없음. 서로 다른 unknown object를 구별하기 위해 clustering accuracy를 기반으로 새로운 평가 방법 unknown mean average precision(UC-mAP)를 제안함.
<img src="https://github.com/zzeuui/papers/assets/38878047/8fea6000-c757-4958-a630-7dc1649cd0f7" width=70%/>
