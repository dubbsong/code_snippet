#### 1. 간단한 컴포넌트

- `render()` 메소드는 데이터를 입력받아 화면에 표시할 내용을 반환한다.
- 컴포넌트로 전달된 데이터는 `render()` 안에서 `this.props`를 통해 접근할 수 있다.

```react
class HelloMessage extends React.Component {
  render() {
    return (
      <div>
        Hello {this.props.name}
      </div>
    );
  }
}

ReactDOM.render(
  <HelloMessage name="Sam" />,
  document.getElementById('hello-example')
);
```

> `Hello Sam`이 출력된다.

<br>

<br>

#### 2. 상태를 가지는 컴포넌트

- 내부적인 상태 데이터는 `this.state`로 접근할 수 있다.
- 컴포넌트의 상태 데이터가 바뀌면 `render()`가 다시 호출되어 마크업이 갱신된다.

```react
class Timer extends React.Component {
  constructor(props) {
    super(props);
    this.state = { seconds: 0 };
  }
  
  tick() {
    this.setState(state => ({
      seconds: state.seconds + 1
    }));
  }
  
  componentDidMount() {
    this.interval = setInterval(() => this.tick(), 1000);
  }
  
  componentWillUnmount() {
    clearInterval(this.interval);
  }
  
  render() {
    return (
      <div>
        Seconds: {this.state.seconds}
      </div>
    );
  }
}

ReactDOM.render(
  <Timer />,
  document.getElementById('timer-example')
);
```

> Seconds가 1씩 증가한다. 

<br>

<br>

#### 3. 애플리케이션

- `state`를 사용해 사용자가 입력한 텍스트와 할 일 목록을 관리한다.
- 이벤트 핸들러들이 inline으로 각각 존재하는 것처럼 보이지만, 실제로는 이벤트 위임을 통해 하나로 구현된다.

```react
class TodoApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = { items: [], text: '' };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  
  render() {
    return (
      <div>
        <h3>TODO</h3>
        <TodoList items={this.state.items} />
        <form onSubmit={this.handleSubmit}>
          <label htmlFor="new-todo">
            What needs to be done?
          </label>
          <input id="new-todo" onChange={this.handleChange} value={this.state.text} />
          <button>
            Add #{this.state.items.length + 1}
          </button>
        </form>
      </div>
    );
  }
  
  handleChange(e) {
    this.setState({ text: e.target.value });
  }
  
  handleSubmit(e) {
    e.preventDefault();
    if (!this.state.text.length) {
      return;
    }
    const newItem = {
      text: this.state.text,
      id: Date.now()
    };
    this.setState(state => ({
      items: state.items.concat(newItem),
      text: ''
    }));
  }
}

class TodoList extends React.Component {
  render() {
    return (
      <ul>
        {this.props.items.map(item => (
          <li key={item.id}>{item.text}</li>
        ))}
      </ul>
    );
  }
}

ReactDOM.render(
  <TodoApp />,
  document.getElementById('todos-example')
);
```

> `TODO`가 구현된다.

<br>

<br>

#### 4. 외부 플러그인을 사용하는 컴포넌트

- React는 유연하다.
- 외부 마크다운 라이브러리인 `remarkable`을 사용해 `<textarea>`의 값을 실시간으로 변환한다.

```react
class MarkdownEditor extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = { value: 'All good?' };
  }
  
  handleChange(e) {
    this.setState({ value: e.target.value });
  }
  
  getRawMarkup() {
    const md = new Remarkable();
    return { __html: md.render(this.state.vlaue) };
  }
  
  render() {
    return (
      <div className="MarkdownEditor">
        <h3>Input</h3>
        <label htmlFor="markdown-content">
          Enter some markdown
        </label>
        <textarea id="markdown-content" onChange={this.handleChange} defaultValue={this.state.value} />
        <h3>Output</h3>
        <div className="content" dangerouslySetInnerHTML={this.getRawMarkup()} />
      </div>
    );
  }
}

ReactDOM.render(
  <MarkdownEditor />,
  document.getElementById('markdown-example')
);
```

> Input의 값이 Output에 실시간으로 반영된다.

<br>

<br>