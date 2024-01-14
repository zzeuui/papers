## Towards Open World Recognition (2015)
CVPR2015

### 💡Problem

1. Open set recognition 문제를 확장해 Open world recognition 문제를 공식적으로 정의
    - Open set recognition(OSR): known과 unknown 클래스를 식별한다
    - Open world recognition(OWR): OSR에 Incremental learning을 적용하여,
      unknown으로 식별된 데이터를 레이블링하여 추가적으로 학습을 진행한다.
2. Open world recognition 문제를 해결하기 위해, incremental learning을 도입함.
   그리고 기존의 incremental learning method인 Nearest Class Mean type algorithms (NCM)을
   open world recognition에 적용할 수 있도록 Nearest Non-Outlier (NNO) algorithm으로 확장하는 방법을 제시.
3. 선형으로 변환된 특징 공간의 거리에 대한 단조롭게 감소하는 함수의 임계값의 합이 임의로 작은 "open space risk"를 가질 수 있음을 보여준다.
   - To support this extension, our third contribution is showing that
     thresholding sums of monotonically decreasing functions of
     distances of linearly transformed feature space can have arbitrarily small “open space risk”. 

### 💡Motivation  
- 기존의 Open set leaning은 one-vs-all batch 방식으로 known과 unknown만 구분하고, 새로운 unknown 데이터로 모델을 확장하지못함
- Novelty detection과 outlier detections는 새로운 클래스를 탐지한 후
  새 클래스를 모델에 학습하기 위해 전체 모델을 다시 학습할 수 있지만,
  이러한 경우 많은 시간과 computational cost가 필요하다.
- Incremental learning을 위한 기존의 방법론인 Distance based classifiers like Nearest Class Mean (NCM)[16, 28, 32]은
  probability normalization을 위해 close-set assumption인 Softmax를 사용하기 때문에 open-set recognition에 적합하지 않다.
  
### 💡Method
#### Nearest Non-Outlier (NNO)
input $x$와 measurable recognition function $f$가 존재할 때, 
$f_{y}(x) \gt 0$이면 $x$의 레이블은 $y$이고, $f_{y}(x) \leq 0$이면 $x$는 unknown임.  
그리고 $\phi=[f_{1}(x), ..., f_{k}(x)]$라고 한다면,
$argmax(\phi)$가 0이면 $x$는 학습하지 못한 레이블을 가진 outlier임.

위 개념을 기반으로 outlier를 측정하기 위한 더 정교한 공식을 제시하기는 하지만,
<img src="https://github.com/zzeuui/papers/assets/38878047/3e17b0b1-b56f-4f1a-8a59-8b148e4d1072"
width=50% />

이 논문의 핵심은,  
1. Open set recognition에 Increamental learning을 적용했다는 것
2. 기존의 Closed set을 위한 Incremental learning의 방법론을 확장하여 적절히 open set learning에 적용했다는 것.
