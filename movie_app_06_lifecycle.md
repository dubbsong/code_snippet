#### Test lifecycle

1. `componentWillMount()`
2. `render()`
3. `componentDidMount()`

<br>

- App.js

```react
...

class App extends Component {
  componentWillMount() {
    console.log('Will mount');	// 테스트 후 제거
  }

  componentDidMount() {
    console.log('Did mount');	// 테스트 후 제거
  }

  render() {
    console.log('Did render');	// 테스트 후 제거
    return (
      <div>
        {movieData.map((movie, index) => {
          return (
            <MovieCard title={movie.title} poster={movie.poster} key={index} />
          );
        })}
      </div>
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

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Test Lifecycle'
$ git push origin master
```

<br>

<br>