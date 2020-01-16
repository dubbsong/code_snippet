#### 개요

- React는 사용자 인터페이스를 구축하기 위한 선언적이고 효율적이며 유연한 JS 라이브러리이다.
- `컴포넌트`라고 불리는 작고 고립된 코드의 파편을 이용하여 복잡한 UI를 구성하도록 돕는다.
- 컴포넌트는 `props`라는 매개변수를 받아오고 `render` 함수를 통해 표시할 뷰 계층 구조를 반환한다.
- `render` 함수는 화면에서 보고자 하는 내용을 반환한다.
- React는 설명을 전달받고 결과를 표시한다.
- JSX 내부의 중괄호 안에 어떤 JS 표현식도 사용할 수 있다.
- React 엘리먼트는 JS 객체이며, 변수에 저장하거나 프로그램 여기저기에 전달할 수 있다.

<br>

#### 세 가지 컴포넌트

1. Square
   - Square 컴포넌트는 `<button>`을 렌더링한다.
2. Board
   - 사각형 9개를 렌더링한다.
3. Game
   - 게임판을 렌더링한다.
   - 나중에 수정할 placeholder 값을 가지고 있다.

<br>

#### props를 통해 데이터 전달하기

- props 전달은, 데이터가 부모에서 자식으로 어떻게 흘러가는지 알려준다.

<br>

1. Square에 `value` prop 전달

```react
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
}
```

<br>

2. 값 표시

```react
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

> 각 사각형에 숫자가 표시된다.

<br>

#### 사용자와 상호작용하는 컴포넌트 생성하기

1. 버튼 태그 변경

```react

```

