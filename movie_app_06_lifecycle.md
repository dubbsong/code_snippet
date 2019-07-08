#### Test lifecycle methods

1. `componentWillMount()` 메소드
2. `render()` 메소드
3. `componentDidMount()` 메소드

<br>

- App.js

```react
...

class App extends Component {
  componentWillMount() {
    console.log('Will mount');	// 확인 후 제거
  }

  componentDidMount() {
    console.log('Did mount');	// 확인 후 제거
  }

  render() {
    console.log('Did render');	// 확인 후 제거
    return (
      ...
    );
  }
}

...
```

> Console tab:
>
> `Will mount`
>
> `Did render`
>
> `Did mount`

> `console.log('...');`를 제거한다.

<br>

#### README.md

```markdown
# Movie App
Learning React and ES6 by building a Movie App.


## Todo
- [x] Add Component
- [x] Set Props
- [x] Set Maping
- [x] Set PropTypes
- [x] Test Lifecycle
- [] Set State
- [] Set Stateless Component
- [] AJAX Networking
- [] Update Component
- [] Styling CSS
- [] Refactoring
- [] Deploying
```

<br>

<br>