## OW-DETR: Open-world Detection Transformer (2022)
CVPR2022  
[[paper](https://openaccess.thecvf.com/content/CVPR2022/papers/Gupta_OW-DETR_Open-World_Detection_Transformer_CVPR_2022_paper.pdf)]
[[code](https://github.com/akshitac8/OW-DETR)]

### 💡Problem
- Deformable DETR기반으로 unknown object를 구분하는 방법을 제안
- unknown object가 background로 인식되는 문제를 완화하기 위해 FC 레이어 추가

### 💡Method
<img src="https://github.com/zzeuui/papers/assets/38878047/46861c78-f36b-4bcf-8d2d-6a5c0f7c7d24" width=80%/>  

1. multi-scale context encoding
Deformable DETR를 베이스 모델로 채택해 다양한 크기의 feature를 활용함

2. attention-driven pseudo-labeling
bipartite matching에서 선택되지 않은 예측들을 backbone의 중간 레이어에서 추출한 feature에 맵핑해 roi를 설정함.
그 후 각 roi의 평균값을 계산해 objectness score로 사용함. 높은 objectness score를 가진 k개의 예측을 unknown으로 지정
(아마 그냥 바운딩 박스안의 feature map 값을 평균하는 것..?)
<img src="https://github.com/zzeuui/papers/assets/38878047/451461be-f964-410a-8fdb-818545c41d3c" width=40%/>  

4. novelty classification
unknown으로 지정된 객체는 (편의상) 0으로 레이블링되어 훈련됨.

5. foreground objectness
unknown으로 지정해도 대부분 background로 예측되어버림. 이 문제를 완화하기 위해 하나의 FC로 구성된 foreground objectness를 추가해서 unknown이 forground임을 훈련함.


