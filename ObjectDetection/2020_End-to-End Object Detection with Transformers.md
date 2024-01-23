## End-to-End Object Detection with Transformers (2020)
ECCV 2020

[[paper](https://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123460205.pdf)]
[[code](https://github.com/facebookresearch/detr)]

### 💡Problem
- 객체 탐지를 direct set prediction 문제로 보는 새로운 방법을 제안
  - prediction과 ground truth가 일대일로 대응되어(bipartitile matching) 손실을 계산함 
- NMS나 앵커 생성을 생략하여 파이프라인을 간소화
- Encoder-Decoder의 구조의 Transformer기반의 모델 제안

### 💡Motivation  
1. 기존 방법의 성능은 중복된 예측을 처리하는 NMS와 앵커 설계에 의해 크게 영향을 받는다.  
$\Rightarrow$ 본 논문에서는 후처리와 휴리스틱을 제거한 end-to-end 방식을 채택한다.

3. 기존 방법도 CNN feature를 기반으로 하는 encoder-decoder 구조와 함께 bipartitie matching losses를 사용한다. 그러나 이러한 방법들은 소규모 데이터셋에 대해서만 평가되었으며, autoregressive model(RNN)을 기반으로한다.  
$\Rightarrow$ 본 논문에서는 병렬 디코딩을 수행하는 Transformer(non-autoregressive)를 사용한다.

### 💡Method

1. Object detection set prediction loss
- Hungarian algorithm을 활용해 prediction과 ground truth를 일대일로 대응해 class와 box에 대한 loss를 계산함.
- anchor를 사용하지 않아 박스 크기에 따른 loss를 계산할 수 없어, bounding box loss를 계산할 때 generalized IoU loss를 포함함.

2. DETR architecture
- Transformer를 기반으로 함
- NLP처럼 출력을 하나씩 예측하는 방식이 아닌(autoregressive), 모든 객체를 동시에 예측하는 방식을 사용(non-autoregressive).
<img src="https://github.com/zzeuui/papers/assets/38878047/e548bec2-6387-443e-96e7-cb4a78064fc2" width=70% >
