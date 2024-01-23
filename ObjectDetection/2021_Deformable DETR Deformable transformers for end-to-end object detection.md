## Deformable DETR: Deformable transformers for end-to-end object detection(2021)
ICLR 2021 Oral  
[[paper](https://arxiv.org/pdf/2010.04159v4.pdf)]
[[code](https://github.com/fundamentalvision/Deformable-DETR)]

### 💡Problem & Motivation  
DETR은 두가지 문제를 가진다:
1. 기존 Object detector보다 수렴하는데 훨씬 긴 학습 시간이 필요함
2.  feature spatial resolution이 제한되어 작은 물체를 탐지하는데 상대적으로 낮은 성능을 가짐

DETR이 가진 Transformer는 가능한 모든 공간의 위치를 조사하려고 해 오랜 학습 시간이 필요함.  
$\Rightarrow$ 이미지 영역에서 이러한 문제를 해결한 deformable convolution과 transformer의 복잡성을 해결하기 위한
data-dependent sparse attention에서 영감을 얻어, reference points 주변에서 샘플링한 points로 구성된 작은 집합으로 attention을 수행하는 Deformable DETR을 제안.

### 💡Method
- **Deformable attention module**: feature map의 공간적 크기와 상관없이 reference point 주변에서 샘플링된 주요 points의 집합에 대해 attention한다. (<=> feature 전체에 대해서 attention하지 않음)
- **Multi-scale deformable attention module**: backbone 네트워크에서 서로 다른 사이즈를 가지는 여러 stage의 feature maps을 사용한다.

<img src="https://github.com/zzeuui/papers/assets/38878047/9ba9db0e-e42d-454e-bb67-6cb39a4976fa" width=90%>

- **Deformable transformer encoder**: 다양한 크기의 feature을 처리하기 위해 1*1 convolution으로 크기를 맞춰준다.
- **Deformable transformer decoder**: self-attetion은 그대로 사용하고, cross-attention부분을 Multi-scale deformable attention module로 대체한다.

### 💡Experiment
- Deformable DETR은 10배 적은 학습 시간으로 DETR보다 더 나은 성능을 달성한다.
