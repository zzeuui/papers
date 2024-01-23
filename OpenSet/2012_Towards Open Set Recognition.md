## Towards Open Set Recognition (2012)
IEEE trans. PAMI

### 💡Problem
positive와 negative뿐만 아니라, unknown도 식별가능한 모델을 제안.

### 💡Motivation  
- 기존의 방법론은 테스트를 할 때 모든 가능한 클래스가 알려진 상태에서 진행되었다.(closed set)
- 이러한 이유로 알려지지 않은 클래스의 경우, 단순히 가장 높은 확률을 가지는 클래스로 잘 못 레이블링 한다.

### 💡Method
Support Vector Machines(SVMs)는 data point들 간의 margin으로 결정된 plane을 두어  postive와 negative 데이터를 분류할 수 있다.

본 논문에서 제안한 SVM의 개념을 확장한 1-vs-set 공식은 decision boundary A 주변에서 핵심적인 margin을 얻고, open set margin을 계산하여 얻은 두번째 평면을 추가하여 unknown 클래스를 찾아낸다.
학습 데이터로 결정된 첫번째 plane으로부터의 empirical risk와 학습 데이터와 unknown데이터로 결정된 두번째 plane으로부터의 open space risk를 결합한 loss function을 최소화한다.  
<img src="https://github.com/zzeuui/papers/assets/38878047/add389a5-02d0-412f-9a4a-69c2b9122262" width=50% />

### 💡Experiment
#### Evaluation Metrics
- Openness: known과 unknown 클래스의 비율로 사용하는 데이터셋이 얼마나 개방적인지 측정함. 0이면 closed set과 동일.
- Accuracy: 정확도
- F1 score: precisioin과 recall의 조화 평균으로, trade-off인 두 지표에 대해 적절히 평가할 수 있음
