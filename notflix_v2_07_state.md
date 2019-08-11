###### 코드 작성: `Container`

- MovieContainer.js

```react
...

export default class extends React.Component {
  state = {
    loading: true,
    nowPlaying: null,
    topRated: null,
    upcoming: null,
    error: null
  };

  // Logic

  render() {
    return (
      <MoviePresenter
        loading={this.state.loading}
        nowPlaying={this.state.nowPlaying}
        topRated={this.state.topRated}
        upcoming={this.state.upcoming}
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
    popular: null,
    topRated: null,
    airingToday: null,
    error: null
  };

  // Logic

  render() {
    return (
      <TVPresenter
        loading={this.state.loading}
        popular={this.state.popular}
        topRated={this.state.topRated}
        airingToday={this.state.airingToday}
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
    detailResult: null,
    error: null
  };

  // Logic

  render() {
    return (
      <DetailPresenter
        loading={this.state.loading}
        detailResult={this.state.detailResult}
        error={this.state.error}
      />
    );
  }
}
```

<br>

<br>