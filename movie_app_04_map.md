#### maping

###### 배열 데이터 통합 / props 설정 / key 설정

- App.js

```react
...

const movieData = [
  {
    title: 'Batman Begins',
    poster: 'https://dummyimage.com/150x200/ff7373/fff'
  },
  {
    title: 'Batman Dark Knight',
    poster: 'https://dummyimage.com/150x200/ffc952/fff'
  },
  {
    title: 'Batman Rises',
    poster: 'https://dummyimage.com/150x200/47b8e0/fff'
  },
  {
    title: 'John Wick',
    poster: 'https://dummyimage.com/150x200/34314c/fff'
  }
];

class App extends Component {
  render() {
    return (
      <div className="App">
        {movieData.map((movie, index) => {
          return (
            <MovieCard
              key={index}
              poster={movie.poster}
              title={movie.title}
            />
          );
        })}
      </div>
    );
  }
}

...
```

> `key` 설정을 하지 않으면, `Warning: Each child in a list should have a unique "key" prop.` 에러가 발생한다.

<br>

#### README.md

```markdown
# Movie App
Learning React and ES6 by building a Movie App.


## Todo
- [x] Add Components
- [x] Set Props
- [x] Set Maping
- [] Set PropTypes
- [] Test Lifecycle
- [] Set State
- [] Set Stateless Component
- [] Set AJAX Networking
- [] Update Component
- [] Styling CSS
- [] Deploying
```

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Set Maping'
$ git push origin master
```

<br>

<br>