---
title: 🥜 [React] Frontend 기술면접 (React)
date: 2024-04-21 08:00:00 +0800
categories: [Frontend, React]
tags: [React, 기술면접]
toc: true
---

> 해당 포스트는 프론트앤드의 기술 면접 중 리액트에 대해 중점적으로 다루는 페이지 입니다.
{: .prompt-tip}

## React

### React 에 대해 설명해주세요.

> Q.
>
> React는 Facebook에서 개발한 JavaScript 라이브러리로, 사용자 인터페이스를 구축하기 위한 라이브러리입니다.
>
> React는 사용자 인터페이스를 만들기 위한 컴포넌트 기반 아키텍처를 사용,
>
> 이를 통해 코드의 재사용성과 유지 보수성을 향상


### React의 원리, 특징, 장단점이 무엇인가요?

> Q.
>
> React 의 핵심 기능
>
> 1) Virtual-DOM
>
> 페이지를 랜더링 할 때 실제 DOM tree 의 변동이 일어날 시 모든 부분을 변경하는 번거로움이 있다.
>
> 하지만 React 는 성능을 향상시키기 위해 가상 DOM 환경을 구축하여
>
> 변경 된 부분만 실제 DOM 에 적용시켜 불필요한 Rerendering 을 방지한다.
>
> 2) JSX 문법
>
> JavaScript 안에 HTML 과 유사한 구조를 갖는 구문을 작성 할 수 있어
>
> 코드의 가독성이 향상되고 재생산성이 증가함


### 라이프사이클에 대해 설명해주세요.

> Q.
>
> 리액트에서의 생명주기는 주로 컴포넌트의 생명주기를 말합니다.
>
> 크게 세가지를 들 수 있습니다.
>
> 1) 마운팅 (Mounting) : 컴포넌트가 DOM 에 삽입 될 때 발생하는 단계
>
> ex) constructor(), render(), componentDidMount()
>
> 2) 업데이팅 (Updating) : 컴포넌트가 업데이트 되고 DOM 에 Re-rendering 될 때 발생하는 단계
>
> ex) render(), componentDidMount()
>
> 3) 언마운팅 (Unmounting) : 컴포넌트가 DOM 에서 제거 될 때 발생하는 단계
>
> ex) componentWillUnmount()

### 함수형 컴포넌트의 장점을 설명해주세요.

> Q. 
>
> 1) 간결성
> 함수형 컴포넌트는 클래스 기반 컴포넌트보다 코드가 간결하고 읽기 쉽습니다.
> 클래스 기반 컴포넌트에서 필요한 boilerplate 코드가 줄어들어서 개발자가 작성해야 할 코드 양이 감소합니다.
>
> 2) 재사용성
>
> 함수형 컴포넌트는 일반 JavaScript 함수이기 때문에 다른 함수와 마찬가지로 재사용이 쉽습니다.
> 이러한 특성으로 인해 컴포넌트의 로직을 분리하고, 재사용 가능한 작은 단위로 구성하는 것이 더욱 쉬워집니다.
>
> 3) 테스트 용이성
>함수형 컴포넌트는 입력값(props)을 받아 출력값을 반환하는 순수 함수
> 이는 함수형 컴포넌트를 테스트하기 쉽게 만들어주며 입력값을 주고 예상 출력값을 확인하는 것이 간단하고 직관적입니다.


### React-Hook 에 대해 설명하세요.

> Q.
>
> 함수형 컴포넌트에서 상태(state) 관리와 React의 기능을 사용할 수 있게 해줍니다.
>
> 또한 상태관리를 간소화 시켜줍니다.
>
> 1) useState : 함수형 컴포넌트에서 상태관리를 할 수 있게 됨
>
> 2) useEffect : 랜더링 시 값을 가져오거나 DOM 조작, 생명주기함수와 비슷하게 동작함
>
> 3) useCallback : 함수를 캐싱하여 랜더링 시 기존 함수를 다시 생성하지 않음
>
> 4) useMemo : 계산비용이 큰 값을 캐싱하여 랜더링 시 다시 계산하지 않도록 함
>
> 5) useRef : DOM 요소에 직접 접근하거나 함수 컴포넌트 내에서 값의 변경을 추적할 때 사용

### 클래스형 컴포넌트에서 함수형 컴포넌트로 변경할 때 생명주기를 어떻게 사용하나요?

> Q.
>
> 1) componentDidMount
> ```js
> // 클래스형 컴포넌트
> class ExampleComponent extends React.Component {
>   componentDidMount() {
>     // 컴포넌트가 마운트된 후에 실행되는 작업
>   }
> }
> // 함수형 컴포넌트
> function ExampleComponent() {
>   useEffect(() => {
>     // 컴포넌트가 마운트된 후에 실행되는 작업
>   }, []);
> }
> ```
> 
> 2) componentDidUpdate
> 
> ```js
> // 클래스형 컴포넌트
> class ExampleComponent extends React.Component {
>   componentDidUpdate(prevProps, prevState) {
>     // 컴포넌트의 props 또는 state가 업데이트될 때 실행되는 작업
>   }
> }
> 
> // 함수형 컴포넌트
> function ExampleComponent({ prop }) {
>   useEffect(() => {
>     // 컴포넌트의 props가 업데이트될 때 실행되는 작업
>   }, [prop]);
> }
> ```
> 
> 3) componentWillUnmount
> 
> ```js
> // 클래스형 컴포넌트
> class ExampleComponent extends React.Component {
>   componentWillUnmount() {
>     // 컴포넌트가 언마운트될 때 실행되는 작업
>   }
> }
> 
> // 함수형 컴포넌트
> function ExampleComponent() {
>   useEffect(() => {
>     return () => {
>       // 컴포넌트가 언마운트될 때 실행되는 작업
>     };
>   }, []);
> }
> 
> ```

### Props Drilling 에 대해 설명해주세요.

> Q. Props Drilling 은 상위 컴포넌트에서 하위 컴포넌트로 props 를 전달하는 과정을 말함 
>
> 일반적으로 컴포넌트 간의 통신을 위해 사용
>
> `장점`
>
> 데이터 흐름이 명확하고 예측 가능합니다.
>
> 컴포넌트 간의 의존성이 낮아지므로 코드 유지보수가 용이합니다.
>
> `단점`
>
> 중간에 있는 컴포넌트들이 데이터에 관여하지 않는 경우에도 데이터가
>
> 계속해서 전달되어야 하므로 성능 저하가 발생할 수 있습니다.
>
> 컴포넌트 구조가 복잡해질수록 Props Drilling이 더 깊어질 수 있고, 이는 코드를 복잡하게 만들 수 있습니다.

### React 에서 Key Props 를 사용하는 이유를 설명해주세요.

> Q.
>
> 해당 이유는 React 의 Virtual DOM 에 그 이유가 존재합니다.
>
> 실제 DOM 에 반영하기 전에 이전 Virtual DOM 과 비교를 하는데,
>
> key 값을 list 에 제공하면 효율적으로 비교하여 관리 및 랜더링을 진행하기 때문입니다.