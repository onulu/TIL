
## 코드 스플리팅?

웹 애플리케이션은 기능이 많아질수록 번들 크기도 커지게 된다. 번들 크기가 커지면 로딩 시간이 증가하고 이로인해 사용성과 SEO에 영향을 주게 된다.

코드스플리팅은 애플리케이션의 **번들**을 여러 개의 작은 청크(chunk)로 나누는 기술로 필요한 코드만 먼저 로드해 페이지 로딩 속도를 개선시킬 수 있다. 큰 번들을 여러개의 작은 청크로 나누고 청크는 실행 시점이나 로직에 따라 그룹화될 수 있다.

`Vite`와 같은 빌드 도구는 별도의 설정 없이도 코드 스플리팅을 기본적으로 동작한다. `Next.js`에서도 코드 스플리팅을 자동으로 지원하며, 페이지 단위로 이루어진다. 각 페이지는 독립적인 청크로 분리된다. 

## React.lazy()

`React.lazy()`는 `import`와 함께 사용해 컴포넌트를 비동기로 로드할 수 있게 해주고 코드 스플리팅을 구현할 수 있다.

아래에서 `LazyModal`컴포넌트는 필요할 때 로드되며, 번들 크기를 줄일 수있다.

```jsx
import { lazy } from 'react'

const LazyModal = lazy(() => import('./SettingsModal'))

function App() {
	const [isSettingsOpen, setSettingsOpen] = React.useState(false)
	
	return (
		<div>
			<button onClick={() => setSettingsOpen(true)}>
			Open Profile Setting
			</button>
			{isSettingsOpen && (
				// Suspense컴포넌트는 비동기 컴포넌트가 렌더링 될때 까지 fallback UI를 보여준다.
				<React.Suspense fallback={<div>Loading..</div>}>
					<LazyModal />
				</React.Suspense>
			)}
		</div>
	)
}
```

무거운 라이브러리를 사용하는 컴포넌트나, 사용자 인증과 관련된 페이지, 조건부로 렌더링되는 광고컨텐츠, 자주 사용되지 않는 기능 등은 **lazy** 와 **동적 import**를 통해 사용시에만 로드하는 것이 앱의 초기 로딩 성능을 크게 개선할 수 있다.


## Suspense

suspense는 흔히 알고 있는 서스펜스 영화? 외에도 사전적으로 일시적 중단, 미결정의 상태, 보류라는 뜻을 가지고 있다.
React에서 `<Suspense>`컴포넌트는 위에서 적용한 동적 import 컴포넌트의 로딩 상태를 관리해주는 컴포넌트이다. 아마도 비동기 컴포넌트가 로드되는 동안 *렌더링을 잠시 보류*한다는 의미로 사용되는것 같다.

`<Suspense>`컴포넌트는 하위 컴포넌트의 비동기 작업이 완료될 때까지 렌더링을 일시 중단하고 `fallback` 파라미터로 받은 UI를 표시한다.
 