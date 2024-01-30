## Random Boxes Are Open-world Object Detectors (2023)
ICCV 2023  
[[paper](https://openaccess.thecvf.com/content/ICCV2023/papers/Wang_Random_Boxes_Are_Open-world_Object_Detectors_ICCV_2023_paper.pdf)]
[[code](https://github.com/scuwyh2000/RandBox)]

### 💡Problem
기존의 방법이 사용한 Faster R-CNN과 DETR이 아닌, Fast R-CNN을 기반으로 하는 RandBox를 제안함.
RandBox는 500개의 bbox를 무작위로 샘플링함. 이러한 방법은 known 객체에 대해서 편향적으로 detector가 학습하는 것을 방지함.
또한 known과 unknown일 확률을 고려한 matching score로 unknown을 식별하여,
known에 치중되지 않고, background와 혼동되지않고 unknown을 판단함.

### 💡Motivation
unknown임에도 known 클래스로 예측되는 경우가 많음. objectness score나 confidence가 높으면 대부분 known instance로 분류됨.
unknown에 대한 실제 레이블이 없어서, 모델은 known에 대해 편향되어짐. 기존의 OWOD 방법은 편향을 해결하지 못함.
unknown과 background가 혼합된 제안은 모두 낮은 신뢰도를 가지고, unknown과 background를 구분하기 어려움.
<img src="https://github.com/zzeuui/papers/assets/38878047/5043be6d-a5e4-4ed0-8563-03d54159a76d" width=60%/>

### 💡Method
1. Random proposals 
훈련의 매 iteration마다 500개의 bbox를 무작위로 생성함. 각 bbox는 [0, 1] 범위에서 4개의 임의의 실수를 샘플링하여 생성됨. 각 숫자는 먼저 표준 Gaussian distribution에서 추출되고 [-2, 2] 범위로 잘린다음 [0, 1] 범위로 선형적으로 조정됨. 이미지 크기에서 벗어난 bbox는 너비와 높이가 조정됨.

2. matching score
known과 unknown 제안에 불이익을 주지 않는 match score를 제안해 더 많은 unknown object를 탐색함.
이미 known 예측은 따로 분류되어 제거되고, 남은 예측에 대해서 unknown을 뽑아내기 위해 다음의 수식을 사용함.
known 클래스와 unknown 클래스에 대한 확률값을 사용해 계산해서 모두 더한 값이 matching score가 됨.
matching score가 크다는 건, 해당 instance가 background보다는 unknown에 가깝다는 걸 의미함
<img src="https://github.com/zzeuui/papers/assets/38878047/c4250d45-a29a-45f1-a00e-42fee2c8496c" width=70%/>

- Fast R-CNN을 기반으로 함
  - Faster R-CNN의 objectness score은 known object에 대해서만 큰 점수를 생성하도록 해서, unknown object에 페널티를 부여함
  - DETR 기반의 방법은 ROI feature의 평균으로 unknown과 background를 구분함. 이 방법은 검증되지 않았으며, unknown이 background로 식별되는 경우가 많음.
  - 제안하는 방법은 known과 unknown을 모두 확인하여 예측을 평가하기 때문에 안정적으로 unknown을 식별할 수 있음.

