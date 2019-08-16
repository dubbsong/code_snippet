###### About TypeScript

- JS의 superset(상위 확장)이다.

- PropTypes는 코드가 실행될 때에만 동작한다.

<br>

<br>

###### 프로젝트 생성

```bash
$ npx create-react-app test --typescript
```

> create-react-app은 `typescript`를 사용할 수 있게 되어 있다.

<br>

<br>

###### styled-components 설치

```bash
$ yarn add @types/styled-components
```

> 보통 `@types/`를 붙여준다.

<br>

<br>

###### test 01

- App.tsx

```react
import React, { Component } from 'react';

interface IState {
  counter: number;
}

class App extends Component<{}, IState> {
  state = {
    counter: 0
  };
  
  add = () => {
    this.setState(prev => {
      return {
        counter: prev.counter + 1
      };
    });
  };
  
  render() {
    return (
      <div>
        {this.state.counter}
        <button onClick={this.add}>Add</button>
      </div>
    );
  }
}

export default App;
```

> 화면의 버튼을 누를 때마다, 1씩 증가한다.

<br>

<br>

###### test 02

- Number.tsx

```react
import React from 'react';
import styled from 'styled-components';

const Container = styled.div``;

interface IProps {
  count: number;
}

const Number = ({ count }) => (
  <Container>{count}</Container>
);

export default Number;
```

> stateless 컴포넌트에서는, `React.FunctionComponent<...>`를 사용한다.

<br>

- App.tsx

```react
import React, { Component } from 'react';
import Number from './Number';

interface IState {
  counter: number;
}

class App extends Component<{}, IState> {
  state = {
    counter: 0
  };
  
  add = () => {
    this.setState(prev => {
      return {
        counter: prev.counter + 1
      };
    });
  };
  
  render() {
    return (
      <div>
        <Number count={this.state.counter} />
        <button onClick={this.add}>Add</button>
      </div>
    );
  }
}

export default App;
```

> 화면의 버튼을 누를 때마다, 1씩 증가한다.

<br>

<br>
