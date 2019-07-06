#### title 설정

###### 배열 데이터 / props 설정 / 콘솔 확인

- App.js

```react
...

const movieTitles = [
  'Batman Begins',
  'Batman Dark Knight',
  'Batman Rises',
  'John Wick'
];

class App extends Component {
  render() {
    return (
      <div>
        <MovieCard title={movieTitles[0]} />
        <MovieCard title={movieTitles[1]} />
        <MovieCard title={movieTitles[2]} />
        <MovieCard title={movieTitles[3]} />
      </div>
    );
  }
}

...
```

<br>

- MovieCard.js

```react
...

class MovieCard extends Component {
  render() {
    console.log(this.props);	// 확인 후 제거한다.
    return (
      ...
    );
  }
}

...
```

> 콘솔에서 props 데이터를 확인할 수 있다.
>
> `console.log(this.props);`를 제거한다.

<br>

#### props 전달

- MovieCard.js

```react
...

class MovieCard extends Component {
  render() {
    return (
      <div>
        <MoviePoster />
        <h2>{this.props.title}</h2>
      </div>
    );
  }
}

...
```

> title이 각각 할당된다.

<br>

#### poster 설정

###### 배열 데이터 / props 설정 / 콘솔 확인

- App.js

```react
...

const moviePosters = [
  'https://dummyimage.com/150x200/ff7373/fff',
  'https://dummyimage.com/150x200/ffc952/fff',
  'https://dummyimage.com/150x200/47b8e0/fff',
  'https://dummyimage.com/150x200/34314c/fff'
];

class App extends Component {
  render() {
    return (
      <div>
        <MovieCard title={movieTitles[0]} poster={moviePosters[0]} />
        <MovieCard title={movieTitles[1]} poster={moviePosters[1]} />
        <MovieCard title={movieTitles[2]} poster={moviePosters[2]} />
        <MovieCard title={movieTitles[3]} poster={moviePosters[3]} />
      </div>
    );
  }
}

...
```

<br>

- MovieCard.js

```react
...

class MovieCard extends Component {
  render() {
    return (
      <div>
        <MoviePoster poster={this.props.poster} />
        ...
      </div>
    );
  }
}

class MoviePoster extends Component {
  render() {
    return <img src={this.props.poster} alt="" />;
  }
}

...
```

> poster가 각각 할당된다.

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Set Props'
$ git push origin master
```

<br>

<br>