###### 코드 작성: `Container`

- MovieContainer.js

```react
...

export default class extends React.Component {
  state = {
    loading: true,
    nowPlaying: null,
    popular: null,
    error: null
  };

  // Logic

  render() {
    return (
      <MoviePresenter
        loading={this.state.loading}
        nowPlaying={this.state.nowPlaying}
        popular={this.state.popular}
        error={this.state.error}
      />
    );
  }
}
```

- TVContainer.js

```react
...

export default class extends React.Component {
  state = {
    loading: true,
    topRated: null,
    popular: null,
    error: null
  };

  // Logic

  render() {
    return (
      <TVPresenter
        loading={this.state.loading}
        topRated={this.state.topRated}
        popular={this.state.popular}
        error={this.state.error}
      />
    );
  }
}
```

- SearchContainer.js

```react
...

export default class extends React.Component {
  state = {
    loading: false, // 맨 처음에 로딩이 필요하지 않다.
    searchWord: '', // 입력을 기다린다.
    movieResults: null,
    tvResults: null,
    error: null
  };

  // Logic

  render() {
    return (
      <SearchPresenter
        loading={this.state.loading}
        searchWord={this.state.searchWord}
        movieResults={this.state.movieResults}
        tvResults={this.state.tvResults}
        error={this.state.error}
      />
    );
  }
}
```

- DetailContainer.js

```react
...

export default class extends React.Component {
  state = {
    loading: true,
    result: null,
    error: null
  };

  // Logic

  render() {
    return (
      <DetailPresenter
        loading={this.state.loading}
        result={this.state.result}
        error={this.state.error}
      />
    );
  }
}
```

<br>

<br>