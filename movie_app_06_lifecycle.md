#### Test lifecycle

1. `componentWillMount()`
2. `render()`
3. `componentDidMount()`

<br>

- App.js

```react
...

const movieData = [...];

class App extends Component {
  componentWillMount() {
    console.log('Will mount');	// 테스트 후 제거
  }

  componentDidMount() {
    console.log('Did mount');	// 테스트 후 제거
  }

  render() {
    console.log('Did renter');	// 테스트 후 제거
    return (
      ...
    );
  }
}

...
```

> Console:
>
> `Will mount`
>
> `Did render`
>
> `Did mount`

> 테스트 후 `console.log(…);`를 제거한다.

<br>

#### README.md

```markdown
# Movie App
Learning React and ES6 by building a Movie App.


## Todo
- [x] Add Components
- [x] Set Props
- [x] Set Maping
- [x] Set PropTypes
- [x] Test Lifecycle
- [] Set State
- [] Set Stateless Component
- [] AJAX Networking
- [] Update Component
- [] Styling CSS
- [] Deploying
```

<br>

<br>