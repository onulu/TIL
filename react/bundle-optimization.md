
## 번들(bundle)?

번들은 여러 개의 자바스크립트 파일과 그 의존성들을 하나의 파일로 결합한 것을 말한다. 여러 파일을 개별적으로 요청하는 대신 하나의 파일로 요청하므로써 HTTP 요청 횟수를 줄일 수 있다. *모듈간 의존성 관리*와 불필요한 코드 제거등의 최적화를 적용하기 용이하다.

### 모듈 간의 의존성

한 모듈이 다른 모듈의 기능을 사용하는 필요관계라고 할 수 있다. 여러 모듈이 얽혀있는 경우에는 각 모듈이 필요로 하는 모듈들을 찾아 연결하고 올바른 순서로 로드하는 것이 중요하다. 


```javascript
// math.js
export function add(a,b) {
	return a + b
}

// utils.js
import { add } from './math.js'
export function addAndSquare(a, b) {
	return add(a, b) ** 2
}

// main.js
import { addAndSquare } from './utils.js'
console.log(addAndSquare(3, 4))
```

위의 코드에서 의존성 그래프는 `main.js -> utils.js -> math.js`와 같이 생성 된다. 이를 바탕으로 모듈을 로드할 순서를 결정한다. 의존하는 모듈은 의존성을 가진 모듈보다 나중에 로드되어야 하기때문에  `math -> utils -> main` 순서로 임포트 되어야 한다.

위의 코드는 번들링 과정을 통해 아래 코드와 같이 의존성 순서대로 import/export문이 실제 함수로 대체되서 조정된다. 

```js
// bundle.js
(function() {
  function add(a, b) {
    return a + b;
  }
  function addAndSquare(a, b) {
    return add(a, b) ** 2;
  }
  console.log(addAndSquare(3, 4));
})();
```

## 번들 사이즈

번들 사이즈는 클라이언트로 전달되는 자바스크립트 코드의 총량을 의미한다. 
번들 사이즈의 측정은 빌드 툴에 따라 다를 수 있지만 `webpack-bundle-analyzer`, `source-map-explorer`등의 툴을 통해 파악할 수 있다.
또는 빌드된 아티팩트의 용량을 직접 분석해서 파악할 수 있다.

어떤 사이즈가 큰지는 정확한 기준은 없지만 실제 서비스에서 네트워크를 통해서는 압축된 크기가 전달되기 때문에 용량을 파악할때는 `gzip`압축 크기를 파악해야 한다. 

## 번들  최적화

### 의존성 관리

- 경량화된 라이브러리 사용
	- `moment.js` 대신 `date-fns`혹은 `dayjs`사용
	- 전체 라이브러리 임포트 대신 함수만 임포트 
		- `import debounce from 'lodash/debounce`
- 중복된 의존성 체크 
	- `dedupe`같은 도구를 통해 중복 제거 할 수 있음

### 코드 관리

- `Polyfill`관리: 폴리필을 포함하는 것만큼이나 필요하지 않은 폴리필을 제거하는 것도 중요하다. `babel-presetpenv`나 `.browserslistrc`파일을 통해서 타겟 브라우저를 설정한다.
- 트리 쉐이킹: ES6 모듈을 활용해 사용되지 않는 코드 제거
- [코드 스플리팅](/react/code-splitting.md)
	- 지연 로딩: `React.lazy()`를 사용

### 에셋 최적화

- 이미지 압축 및 사이즈 최적화
- 이미지에 `lazy-loading`구현

### 빌드 관리

- 빌드 프로세스에 `minification` 적용
- 빌드 툴 내부의 설정 최적화
- 번들 사이즈 모니터링
	- CD/CI 파이프라인에 모니터링 추가

