
# openCV에서 카메라 연동하기

1. 카메라를 연다.
  `cap = cv2.VideoCapture(0)` - 0 은 카메라 번호를 나타내고 파일을 재생할때는 파일 경로를 입력한다.
2. 캡쳐 환경을 설정한다.
   1. `cap.set`을 사용해 원하는 기본 설정값을 변경한다.
   2. `FRAME_WIDTH`, `FRAME_HEIGHT`, `FPS`등
3. 카메라가 잘 실행되었는지 `isOpened()`를 통해 확인한다.
4. 캡쳐를 읽는다. (`while` 문을 통해 구현)
5. cap의 반화값으로 `ret` `frame`을 가져오고
   1. `ret`가 있는 경우에 `imshow`메서드로 프레임을 새창에서 보여줄 수 있다.
6.  카메라 사용이 끝나면 카메라를 릴리즈한다. `cap.release()`
7.  윈도우를 닫는다. `cv2.destroyAllWindows()`

```python

import cv2
# 1. 카메라 열기
cap = cv2.VideoCapture(0)

# 2. 캡처 환경 설정
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 640)
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 480)
cap.set(cv2.CAP_PROP_FPS, 30)

# 3. 카메라가 정상적으로 열렸는지 확인
if not cap.isOpened():
    print("카메라가 열리지 않았습니다.")
    exit()

# 4. 프레임을 읽고 표시
while True:
    ret, frame = cap.read()  # 프레임 읽기
    if ret:
        cv2.imshow("Camera Feed", frame)  # 화면에 프레임 표시
    if cv2.waitKey(1) & 0xFF == ord('q'):  # 'q'를 누르면 종료
        break

# 5. 카메라 및 창 닫기
cap.release()
cv2.destroyAllWindows()
```
