# Affine transformation

`warpAffine`은 이미지 변환을 위한 함수로, 이미지를 변환시킬 때 사용된다.
**Affine transformation (아핀 변환)** 은 평행선이나 선형 구조를 유지하면서 변형을 허용하는 변환의 성격을 가진다. 이동, 회전, 스케일링(scaling), 기울기(shear)을 적용할 수 있으며 변환이 일어날 때에도 기본적인 형상이 크게 왜곡되지 않는다. (직선성과 평행성을 유지한다.)

*변환 후에도 직선이 직선으로 남는다는 것이 왜 중요한가?*
아핀편환은 이미지의 직선들을 구부러지거나 왜곡하지 않고 여전히 직선인 상태로 유지한다. 이미지의 중요한 기하학적 특성을 변환 후에도 유지할 수 있다는 것이다.

## warpAffine 사용하기

```python
cv2.warpAffine(
	src, # 원본 이미지
	M, # 아핀변환 행렬
	dsize, # 결과 이미지의 크기 (w, h)
	flags=cv2.INTER_LINEAR, # interpolation방법
	borderMode, # 경계 처리 방식
	borderValue # 경계 픽셀 값 (0)
)
```

## 아핀변환 행렬

2x3의 크기의 행렬을 사용한다.

```python
M = [[a, b, tx],
	 [c, d, ty]]
```

- `(tx, ty)`: 평행 이동을 나타냄
- `a, b, c, d`: 회전, 스케일링, 기울기등의 선형 변환 성분을 나타냄

## 변환 공식

변환된 좌표  $(x{\prime}, y{\prime})$는 원본 좌표  $(x, y)$ 와 변환 행렬  $M$ 을 사용해 다음과 같이 계산된다.

$$
\begin{bmatrix} x{\prime} \\ y{\prime} \end{bmatrix} = M \cdot \begin{bmatrix} x \\ y \\ 1 \end{bmatrix} = \begin{bmatrix} a & b & tx \\ c & d & ty \end{bmatrix} \cdot \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}
$$

**회전 행렬**은 다음과 같다. 이미지를 $\theta$ 만큼 회전 시킨다.
$$
M = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \end{bmatrix}
$$

**스케일링 행렬** - sx는 x축의 스케일을 sy는 y축의 스케일 비율을 나타낸다.
$$
M = \begin{bmatrix} sx & 0 & 0 \\ 0 & sy & 0 \end{bmatrix}
$$
**기울기 행렬** - shx는 x축 기울기, shy는 y축 기울기를 나타낸다.
$$
M = \begin{bmatrix} 1 & sh_x & 0 \\ sh_y & 1 & 0 \end{bmatrix}
$$
**평행 이동**  - tx는 x축으로의 이동, ty는 y축으로의 이동을 나타낸다.
$$
M = \begin{bmatrix} 1 & 0 & tx \\ 0 & 1 & ty \end{bmatrix}
$$

## openCV에서 변환 행렬 정의하기

직접 행렬의 정의하거나 `getRotationMatrix2D`를 사용해 회전행렬을 생성할 수 있다.

```python
# x축으로 50, y축으로 10 이동
M = np.float32([[1, 0, 50], [0, 1, 10]])

# 이미지 처리나 기하학 변환에서는 float32(32비트 부동소수점)를 주로 사용함
```

회전행렬 함수로 구하기

```python
center = (width // 2, height // 2)
angle = 45
scale = 1.0

M = cv2.getRotationMatrix2D(center, angle, scale)
```
