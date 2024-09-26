# Rotation Matrix 사용해서 rotate적용하기

이미지를 회전할때 `RotationMatrix`를 활용하면 잘리는 부분없이 안전하게 회전시킬 수 있다.
`RotationMatrix`는 2D공간에서 점이나 벡터를 회전시킬 때 사용되는 `2x3` 행렬이다. 각각의 요소는 다음과 같다.

```python
[[ cos θ  -sin θ  tx ]
 [ sin θ   cos θ  ty ]]
```

- `θ` 회전 각도
- `(tx, ty)`: translation 벡터, 이동벡터로 회전 후 중심을 조정하는데 사용되는 값

## RotationMatrix 생성하기

```python
rotation_matrix = cv2.getRotationMatrix2D(center, angle, scale)
```

- center: 회전 중심축 `(x,y)`
- angle: 회전 각도 (양수는 반시계 방향을 나타냄)
- scale: 스케일 배수

### RotationMatrix 조정하기

회전 후 이미지가 잘리기 않게 하려면 translation 부분 `(tx, ty)` 를 회전된 이미지가 담길 수 있는 사이즈에 맞춰 조정한다.

```python
# 정사각형을 회전했을 때 가장 커질 수 있는 사이즈는, 대각선을 양변으로 가지는 정사각형의 사이즈가 된다. 좀 더 세밀한 조정을 하려면 sin, cos를 활용한다.
diagonal = int(np.ceil(np.sqrt(width**2 + height**2)))

# [0, 2]는 tx값
rotation_matrix[0, 2] += (diagonal - width) // 2

# [1, 2]는 ty값
rotation_matrix[1, 2] += (diagonal - height) // 2
```
