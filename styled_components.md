### create-react-app 생성

```bash
$ npx create-react-app styled_components
```

<br>

### VSCode 열기

```bash
$ cd styled_components
$ code .
```

<br>

### 코드 수정

- public/index.html

```html
<title>Styled Components</title>
```

<br>

### 파일 삭제

- src/App.css
- src/App.test.js
- src/index.css
- src/logo.svg
- serviceWorker.js

<br>

- index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

<br>

- App.js

```react
import React, { Component } from 'react';

class App extends Component {
  render() {
    return <div>test</div>;
  }
}

export default App;
```

<br>

### react 실행

- terminal

```bash
$ yarn start
```

> 화면에 `test`가 표시된다.

<br>

### 파일 생성

- src/App.css

<br>

### 코드 추가

- App.css

```css
.button {
  font-size: 1em;
  font-weight: 600;
  color: #ffffff;
  width: 120px;
  height: 40px;
  margin: 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.button:active,
.button:focus {
  outline: none;
}

.button_yes {
  background-color: #2980b9;
}

.button_no {
  background-color: #c0392b;
}
```

<br>

- App.js

```react
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div>
        <button className="button button_yes">YES</button>
        <button className="button button_no">NO</button>
      </div>
    );
  }
}

export default App;
```

<br>

> **여기까지는 과거에 사용하던 방식이다.**

------

<br>

### styeld-components 설치

- terminal

```bash
$ yarn add styled-components
$ yarn start
```

<br>

### 코드 수정 및 추가

- App.js

```react
import React, { Component } from 'react';
import styled from 'styled-components';

class App extends Component {
  render() {
    return (
      <Container>
        <Button>YES</Button>
        <Button no>NO</Button>
      </Container>
    );
  }
}

const Container = styled.div`
	width: 100%;
	height: 100vh;
	background-color: #20a19c;
`;

const Button = styled.button`
	font-size: 1em;
	font-weight: 600;
	color: #ffffff;
	width: 120px;
	height: 40px;
	margin: 20px;
	border: none;
	border-radius: 5px;
	cursor: pointer;
	&:active,
	&:focus {
		outline: none;
	}
	background-color: ${props => (props.no ? '#c0392b' : '#2980b9')};
`;

export default App;
```

<br>

### 파일 제거

- src/App.css

<br>

> 과거에 사용하던 방식과 동일하게 표시된다.

------

<br>

### createGlobalStyle 사용하기 (body margin 제거)

- App.js

```react
import React, { Component } from 'react';
import styled, { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
	body {
		padding: 0;
		margin: 0;
	}
`;

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <GlobalStyle />
        <Container>
          <Button>YES</Button>
          <Button no>NO</Button>
        </Container>
      </React.Fragment>
    );
  }
}

const Container = styled.div`
	width: 100%;
	height: 100vh;
	background-color: #20a19c;
`;

const Button = styled.button`
	font-size: 1em;
	font-weight: 600;
	color: #ffffff;
	width: 120px;
	height: 40px;
	margin: 20px;
	border: none;
	border-radius: 5px;
	cursor: pointer;
	&:active,
	&:focus {
		outline: none;
	}
	background-color: ${props => (props.no ? '#c0392b' : '#2980b9')};
`;

export default App;
```

<br>

### 컴포넌트 재활용 (extension)

- App.js

```react
import React, { Component } from 'react';
import styled, { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
	body {
		padding: 0;
		margin: 0;
	}
`;

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <GlobalStyle />
        <Container>
          <Button>YES</Button>
          <Button no>NO</Button>
          <Anchor href="https://dubbsong.github.io">오많배</Anchor>
        </Container>
      </React.Fragment>
    );
  }
}

const Container = styled.div`
	width: 100%;
	height: 100vh;
	background-color: #20a19c;
`;

const Button = styled.button`
	font-size: 1em;
	font-weight: 600;
	color: #ffffff;
	width: 120px;
	height: 40px;
	margin: 20px;
	border: none;
	border-radius: 5px;
	cursor: pointer;
	&:active,
	&:focus {
		outline: none;
	}
	background-color: ${props => (props.no ? '#c0392b' : '#2980b9')};
`;

const Anchor = styled(Button.withComponent('a'))`
	text-decoration: none;
`;

export default App;
```

<br>

### 회전 애니메이션 적용하기

- App.js

```react
import React, { Component } from 'react';
import styled, { createGlobalStyle, css, keyframes } from 'styled-components';

const GlobalStyle = createGlobalStyle`
	body {
		padding: 0;
		margin: 0;
	}
`;

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <GlobalStyle />
        <Container>
          <Button>YES</Button>
          <Button no>NO</Button>
          <Anchor href="https://dubbsong.github.io">오많배</Anchor>
        </Container>
      </React.Fragment>
    );
  }
}

const Container = styled.div`
	width: 100%;
	height: 100vh;
	background-color: #20a19c;
`;

const Button = styled.button`
	font-size: 1em;
	font-weight: 600;
	color: #ffffff;
	width: 120px;
	height: 40px;
	margin: 20px;
	border: none;
	border-radius: 5px;
	cursor: pointer;
	&:active,
	&:focus {
		outline: none;
	}
	background-color: ${props => (props.no ? '#c0392b' : '#2980b9')};
	${props => {
    if (props.no) {
      return css `animation: ${rotation} 2s linear infinite`;
    }
  }}
`;

const Anchor = styled(Button.withComponent('a'))`
	text-decoration: none;
`;

const rotation = keyframes`
	from {
		transform: rotate(0deg);
	}
	to {
		transform: rotate(360deg);
	}
`;

export default App;
```

------

<br>

<br>

### Attributes 설정

- App.js

```react
import React, { Component } from 'react';
import styled, { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
	body {
		padding: 0;
		margin: 0;
	}
`;

const Input = styled.input.attrs({
  required: true
})`
	border: none;
`;

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <GlobalStyle />
        <Container>
          <Input placeholder="todo" />
        </Container>
      </React.Fragment>
    );
  }
}

const Container = styled.div`
	width: 100%;
	height: 100vh;
	background-color: #20a19c;
`;

export default App;
```

<br>

### Mixins 설정

- App.js

```react
import React, { Component } from 'react';
import styled, { createGlobalStyle, css } from 'styled-components';

const GlobalStyle = createGlobalStyle`
	body {
		padding: 0;
		margin: 0;
	}
`;

const awesomeCard = css`
	box-shadow: 0 4px 6px rgba(50, 50, 93, 0.11) 0 1px 3px rgba(0, 0, 0, 0.08);
	background-color: #ffffff;
	padding: 20px;
	border-radius: 10px;
`;

const Input = styled.input.attrs({
  required: true
})`
	border: none;
	${awesomeCard}
`;

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <GlobalStyle />
        <Container>
          <Input placeholder="todo" />
        </Container>
      </React.Fragment>
    );
  }
}

const Container = styled.div`
	width: 100%;
	height: 100vh;
	background-color: #20a19c;
`;

export default App;
```

<br>

<br>

### Theme 설정

- src/theme.js 생성

<br>

- theme.js

```react
const theme = {
  mainColor: '#1abc9c',
  noColor: '#c0392b',
  yesColor: '#2980b9'
};

export default theme;
```

<br>

- App.js

```react
import React, { Component } from 'react';
import styled, { createGlobalStyle, ThemeProvider } from 'styled-components';
import theme from './theme';

const GlobalStyle = createGlobalStyle`
	body {
		padding: 0;
		margin: 0;
	}
`;

const Container = styled.div`
	width: 100%;
	height: 100vh;
	background-color: #20a19c;
`;

const Card = styled.div`
	background-color: #998ac5;
`;

const Button = styled.button`
	background-color: ${props => props.theme.noColor};
	width: 120px;
	height: 40px;
	border-radius: 5px;
`;

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <GlobalStyle />
        <ThemeProvider theme={theme}>
          <Container>
            <Form />
          </Container>
        </ThemeProvider>
      </React.Fragment>
    );
  }
}

const Form = () => (
  <Card>
    <Button>What's up?</Button>
  </Card>
);

export default App;
```

<br>

### Nesting

- App.js
  - ex: Form 내의 모든 Card를 선택해서 변경하고 싶다면,

```react
import React, { Component } from 'react';
import styled, { createGlobalStyle, ThemeProvider } from 'styled-components';
import theme from './theme';

const GlobalStyle = createGlobalStyle`
	body {
		padding: 0;
		margin: 0;
	}
`;

const Card = styled.div`
	background-color: #998ac5;
`;

const Container = styled.div`
	width: 100%;
	height: 100vh;
	background-color: #20a19c;
`;

const Button = styled.button`
	background-color: ${props => props.theme.noColor};
	width: 120px;
	height: 40px;
	border-radius: 5px;
`;

class App extends Component {
  render() {
    return (
      <React.Fragment>
        <GlobalStyle />
        <ThemeProvider theme={theme}>
          <Container>
            <Form />
          </Container>
        </ThemeProvider>
      </React.Fragment>
    );
  }
}

const Form = () => (
  <Card>
    <Button>What's up?</Button>
  </Card>
);

export default App;
```

<br>

> Card가 Container 보다 위에 선언되어야 정상 작동

<br>