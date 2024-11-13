# Underfit & Overfit

## 과소적합 (Underfit)

모델이 학습 데이터에 대해 너무 단순화된 결론을 내리는 것으로 데이터의 복잡성을 제대로 학습하지 못해 낮은 성능을 보이는 현상

### 원인

- 모델이 너무 간단하거나 학습 데이터가 부족할때
- 데이터의 중요한 특징을 제대로 반영하지 못했을 경우 발생
- 훈련 및 테스트 데이터셋에서 모두 높은 오차와 낮은 정확도를 보일때

*예) Linear Regression을 복잡한 비선형 데이터에 적용했을때 발생할 수 있음.*

### 해결방안

- 좀 더 복잡한 모델을 사용한다.
- 더 많은 피쳐를 사용하여 모델이 학습할 수 있는 정보를 늘림
- 더 많은 데이터를 사용하거나 학습 시간을 연장한다.

---

## 과대적합 (Overfit)

모델이 학습 데이터에 과도하게 맞춰져서, 학습 데이터에서는 높은 성능을 보이지만, 새로운 데이터에 대해서는 일반화하지 못해 성능이 저하되는 현상

### 과적합의 원인

- 모델이 지나치게 복잡하고 학습 데이터를 너무 많이 학습했을 때 발생
- 데이터에 있는 노이즈나 이상치를 과도하게 반영하여 새로운 데이터에 대해 일반화하지 못하는 경우
- 훈련 데이터셋에서의 에러는 매우 낮지만 테스트 데이터셋에서 높은 오차가 나타나는 경우

### 과적합 해결방안

- 모델의 복잡도를 줄인다.
- L1, L2등의 규제를 적용한다.
- 교차 검증 (K-n fold)
