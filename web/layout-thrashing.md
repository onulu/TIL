
# Layout Thrashing

Layout Thrashing은 브라우저가 실제 필요한 작업보다 **레이아웃 계산**에 더 많은 자원을 소비하는 현상을 말한다.
브라우저는 DOM이 수정될 때마다 레이아웃을 다시 계산해야 하는데, 이 과정이 불필요하게 여러 번 반복되면 성능이 저하된다.
Layout최적화는 웹 성능 지표중 하나인 INP(Interaction to Next Paint)를 개선하는데 중요하다.

**INP**는 웹페이지와 상호작용에 대한 응답성을 측정하는 메트릭이다. 사용자가 페이지와 상호작용한 후 다음 프레임이 화면에 그려지기까지의 지연시간을 측정한다.
Layout Thrashing은 메인 스레드를 차단해 사용자 상호작용에 대한 응답을 지연시킨다. 레이아웃 재계산은 비용이 크기때문에 이는 INP값을 증가시킬 수 있다.

DOM요소 레이아웃에 대한 읽기와 쓰기 작업이 반복적으로 섞여 있을 때 발생한다.

```js
// 마우스를 따라다니는 툴팁을 만들어보자
const tooltip = document.createElement('div');
tooltip.className = 'tooltip';
tooltip.innerHTML = '툴팁';
document.body.appendChild(tooltip);

document.addEventListener('mousemove', (e) => {
    const width = tooltip.offsetWidth;   // 읽기 - forced reflow 발생
    const height = tooltip.offsetHeight;  // 읽기 - forced reflow 발생
    
    tooltip.style.left = (e.pageX - width / 2) + 'px';   // 쓰기 - 레이아웃 무효화
    tooltip.style.top = (e.pageY - height - 10) + 'px';  // 쓰기 - 레이아웃 무효화
});
```

`mousemove`이벤트 리스너에서 마우스가 움직일때마다 layout에 대한 읽기와 쓰기가 반복적으로 읽어나게 되고 layout thrashing이 발생하게 된다.
`requestAnimationFrame`을 사용하거나 transform을 사용해 개선할 수 있다.

1. transform 사용

`transform`은 레이아웃을 트리거하지 않고 composite만을 트리거하는 속성이므로 layout thrashing이 발생하지 않는다.

```js
const tooltip = document.createElement('div');
tooltip.className = 'tooltip';
tooltip.innerHTML = '툴팁';
document.body.appendChild(tooltip);

// 초기에 한 번만 크기 측정
const { width, height } = tooltip.getBoundingClientRect();

document.addEventListener('mousemove', (e) => {
    // transform 사용으로 레이아웃 재계산 회피
    const x = e.pageX - width / 2;
    const y = e.pageY - height - 10;
    tooltip.style.transform = `translate(${x}px, ${y}px)`;
});
```

2. `requestAnimationFrame`응 사용해 업데이트를 제어

requestAnimationFrame은 브라우저 렌더링 주기에 맞춰 애니메이션을 실행하는 메서드이다.
비활성탭에서는 실행이 중지되고 브라우저의 렌더링 주기에 맞춰 실행된다.

```js
const tooltip = document.createElement('div');
tooltip.className = 'tooltip';
tooltip.innerHTML = '툴팁';
document.body.appendChild(tooltip);

// 초기에 한 번만 크기 측정
const { width, height } = tooltip.getBoundingClientRect();

let rafId;
document.addEventListener('mousemove', (e) => {
    // 프레임당 한 번만 실행
    cancelAnimationFrame(rafId);
    rafId = requestAnimationFrame(() => {
        tooltip.style.transform = `translate(${e.pageX - width/2}px, ${e.pageY - height - 10}px)`;
    });
});
```

## 최적화 하기

- Layout 속성의 읽기와 쓰기 작업을 분리
- CSS 인터렉션 적용시 레이아웃을 트리거 하는 속성을 최소화
- will-change 속성을 사용해 브라우저에게 변경될 속성을 미리 알려줌으로써, 브라우저가 사전에 최적화를 준비할 수 있게 한다.
- 복잡한 애니메이션은 absolute나 fixed 포지셔닝을 사용하면 요소가 일반적 문저 스름에서 제거된다. 해당 요소의 변경이 다른 요소의 레이아웃 재계산을 트리거 하지 않게 된다.
