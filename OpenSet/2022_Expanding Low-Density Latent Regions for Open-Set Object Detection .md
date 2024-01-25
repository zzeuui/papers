## Expanding Low-Density Latent Regions for Open-Set Object Detection (2022)
CVPR2022  
[[paper](https://openaccess.thecvf.com/content/CVPR2022/papers/Han_Expanding_Low-Density_Latent_Regions_for_Open-Set_Object_Detection_CVPR_2022_paper.pdf)]
[[code](https://github.com/csuhan/opendet2)]

### 💡Problem
unknown object가 클러스터링 된 잠재 공간에서 일반적으로 low density space에 분포한다는 합의를 바탕으로,
high/low desity latent space를 더욱 분리하여 unknown을 식별하는 Open-set Detector(OpenDet)을 제안함.

### 💡Motivation  
known object는 latent space에서 고밀도 영역을 형성하고, unknown object는 저밀도 영역에 분포된다.  
즉, unknown object를 식별하기 위해 고밀도와 저밀도 잠재 영역을 적절히 분리하는 것이 중요하다.  
그러나 기존의 threshold-based methods는 모든 unknown object를 포함할 수 없는 제한된 low density regions만을 가짐
<img src="https://github.com/zzeuui/papers/assets/38878047/1443f7a4-0782-4718-a410-9683272b85ff" width=60%/>

### 💡Method
**CFL(Contrastive Feature Learner)**: known object의 feature에 대해서 instance level의 contrastive learning을 수행해
known object가 좀 더 밀집되도록하여 unknown object를 위한 더 많은 저밀도 영역을 남겨둠.  
**UPL(Unknown Probability Learner)**: 예측의 불확실성으로 unknown object의 probability를 계산해 최적화해서
known object의 클러스터 주변의 저밀도 영역을 더 나눔

<img src="https://github.com/zzeuui/papers/assets/38878047/9cf128b7-de82-4da4-b16b-8d955dff63ea" width=30%/>

#### 1. baseline setup  
- Faster R-CNN을 사용해서 클래스와 바운딩 박스 예측. 클래스는 scaled cosine similarity scores로 확률 계산

#### 2. contrastive feature learner
- contrastive head: multilayer perceptron으로 Faster R-CNN에서 나온 feature의 dimension을 낮춤
- class-balanced memory bank: contrastive learning에서 negative sample 수가 많을 수록 좋은데, 그러면 메모리가 많이 필요해서 도입된 방법이 memory bank임. memory bank는 샘플의 다양성을 증가시킴. 그리고 여기서 더 나아가 본 논문에서 객체의 다양성도 증가시키기 위해 이 방법을 제안함
- instance-level contrastive learning: ICLoss를 제안하는데, 한 feature의 loss를 계산하기 위해 memory bank에 있는 동일한 클래스를 가지는 다른 feature를 사용함
  $\Rightarrow$ unknown객체를 훈련에 사용할 수 없지만, known클래스를 분리하면 unknown을 식별하는데 도움이 됨. 이러한 loss 계산 방식은 known 클래스의 클러스터를 low density latent regions에서 멀리 밀어내는 효과가 있음.

#### 3. unknown probability learner
- known class의 클러스터 주위의 low density latent regions을 더 나누기 위해 제안.
- 정답값이 없는 unknown에 대한 entropy 값을 계산하기 위한 수식을 소개하는데... 이해 못하겠음...
  - 높은 entropy 값을 가지는 상위 example로 unknown probability를 정의..?
  - 모든 클래스의 최대 확률은 또다른 불확실성의 신호이기 때문에, minimum max probability를 갖는 상위 예제로 unknown probability를 정의...?
- 그리고 이러한 unknown probability는 known의 cross entropy가 수렴하는데 불이익을 주기 때문에 가중치를 더해줌.

