
# PyTorch

## Tensor

### 텐서의 정의

- 텐서는 배열이나 행렬과 매우 유사한 자료구조이다.
- numpy배열과 비슷하지만 GPU를 지원해서 딥러닝 계산에 최적화되어 있다
- 텐서는 0차원(스칼라)부터 N차원까지의 배열을 의미한다.
	- 0차원: 스칼라
	- 1차원 텐서: 벡터 `[1.0, 2.0]`
	- 2차원 텐서: 행렬 `[[1.0, 2.0], [3.0, 4.0]]`
	- 3차원 이상: 영상이나 이미지의 고차원 데이터

### 텐서 생성하기

```python
import torch

t1 = torch.tensor([1, 2, 3])
t2 = torch.tensor([[1, 2], [3, 4]])

t_random = torch.randn((3, 3)) # 3x3의 랜덤 텐서
```

### GPU지원

`.cuda()`를 사용해 텐서 연산을 GPU를 사용해 가속화 할 수 있다. 

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
t_gpu = torch.tensor([1, 2], device=device)
print(t_gpu)
```

### Autograd

- 자동 미분 / 동적 계산 그래프
- PyTorch는 연산을 할 때마다 그래프가 즉석으로 만들어지고, 그걸 기반으로 [역전파](backpropagation.md)를 통해 자동으로 기울기(gradient)를 계산한다.

### NCHW

`N, C, H, W` 는 딥러닝에서 텐서의 데이터 포맷을 나타내는 형식 중 하나다. 특히, CNN에서 자주 사용됀다.

- **N** - Batch size 입력 데이터의 배치 크기
- **C** - Channels 채널, 이미지의 경우 색상 채널
- **H** - 이미지의 세로 크기
- **W** - 가로 크기

---

## 단순 선형 회귀 학습하기

선형모델 
`y = Wx + b`

- y: 예측값
- W: 가중치
- x: 입력값
- b: 편향


1. 필요한 라이브러리 가져오기

```python
import torch
import torch.nn as nn
import torch.optim as optim
```

2. 샘플 데이터 세트 생성

`y = 2x + 3 + noise` 를 가지고 선형회귀를 학습해본다.

```python
import torch
import torch.nn as nn
import torch.optim as optim

# 입력 데이터(x)와 타깃 데이터(y)를 생성
x_train = torch.linspace(0, 10, steps=100).unsqueeze(1)  # (100, 1) 크기의 텐서
y_train = 2 * x_train + 3 + torch.randn_like(x_train)  # 실제 관계는 y = 2x + 3 + 노이즈


# 모델 정의
model = nn.Linear(in_features=1, out_features=1)

# 손실 함수 및 옵티마이저 정의
criterion = nn.MSELoss()
learning_rate = 0.01
optimizer = optim.SGD(model.parameters(), lr=learning_rate)

# 학습
num_epochs = 1000

for epoch in range(num_epochs):
    outputs = model(x_train)
    loss = criterion(outputs, y_train)
    
    optimizer.zero_grad() # 이전 배치에서 계산된 그래디언트를 초기화한다.
    loss.backward() # 역전파를 수행하여 각 파라미터에 대한 그래디언트 계산
    optimizer.step() # 파라미터를 업데이트
    
    if (epoch+1) % 100 == 0:
        print(f'Epoch [{epoch+1}/{num_epochs}], Loss: {loss.item():.4f}')

# 학습된 가중치와 편향 출력
print(f'Learned weight: {model.weight.item():.4f}, Learned bias: {model.bias.item():.4f}')
```

## 역전파

역전파는 신경망 학습에서 손실 함수로부터 모델의 가중치와 편향에 대한 그래디언트(기울기)를 계산하는 과정이다. 그래디언트는 옵티마이저가 가중치를 업데이트하여 손실 함수를 최소화하는 데 사용된다.

손실함수로부터 기울기를 계산하는것

손실함수 - 회귀 문제에서는 주로 MSE를 사용
그래디언트 - 가중치와 편향에 대한 손실 함수의 변화율 (함수의 미분)

손실 함수 L을 모델의 각 파라미터에 대해 미분하여 기울기를 구한다. 
이 그래이언트를 사용해 파라미터를 업데이트함으로써 손실을 최소화한다.

파이토치에서 역전파과정

1. 순전파 forward pass
	- 입력 데이터를 모델이 통과시켜 예측값을 계산
	- 모든 연산은 계산 그래프에 기록됨
2. 손실 계산
	- 예측값과 실제값 사이의 손실을 계산. 손실은 스칼라 값이며, 계산 그래프의 마지막 노드
3. loss.backward()
	- 역전파를 시작
	- 계산 그래프의 마지막 노드(손실)부터 시각하여 각 노드에 대한 그래디언트(기울기)를 계산
4. 자동 미분  Auto-grad
	- autograd엔진이 그래디언트 계산을 자동으로 수행
	-  backward() 안에서 자동 실행
5. 그래디언트 축적
	1. 계산된 그래디언트는 각 파라미터의 grad속성에 누적된다.
	2. 따라서 매번 optimizer.zero_grad()로 초기화해야함
