#### react-lines-ellipsis 설치 (for …)

```bash
$ yarn add react-lines-ellipsis
```

<br>

- Usage

```react
import LinesEllipsis from 'react-lines-ellipsis';

<LinesEllipsis
  text={props}
  maxLine='3'
  ellipsis='...'
  trimRight
  basedOn='letters'
/>
```

> [react-lines-ellipsis](https://www.npmjs.com/package/react-lines-ellipsis) 참조

<br>

- MovieCard.js

```react
...
import LinesEllipsis from 'react-lines-ellipsis';

function MovieCard({ poster, title, genres, synopsis }) {
  return (
    <div className="Movie__Card">
      ...
        <div className="Movie__Synopsis">
          <LinesEllipsis
            text={synopsis}
            maxLine="5"
            ellipsis="..."
            trimRight
            basedOn="letters"
          />
        </div>
      ...
    </div>
  );
}

...
```

<br>

#### CSS

- index.css

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
    Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  height: 100%;
  margin: 0;
}

html,
#root {
  height: 100%;
}
```

<br>

- App.css

```css
.App {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  font-size: 14px;
  padding: 50px;
}

.App--loading {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
```

<br>

- MovieCard.css

```css
.Movie__Card {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: flex-start;
  text-overflow: ellipsis;
  background-color: #ffffff;
  width: 40%;
  padding: 0 20px;
  margin-bottom: 50px;
  box-shadow: 0 8px 38px rgba(133, 133, 133, 0.3),
    0 5px 12px rgba(133, 133, 133, 0.22);
}

.Movie__Column {
  text-overflow: ellipsis;
  width: 30%;
  box-sizing: border-box;
}

.Movie__Column:last-child {
  width: 60%;
  padding: 20px 0;
}

.Movie__Card h2 {
  font-size: 20px;
  font-weight: 600;
}

.Movie__Card .Movie__Genres {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.Movie__Genres .Movie__Genre {
  color: #b4b5bd;
  margin-right: 10px;
}

.Movie__Card .Movie__Synopsis {
  text-overflow: ellipsis;
  color: #b4b5bd;
  overflow: hidden;
}

.Movie__Card .Movie__Poster {
  position: relative;
  max-width: 100%;
  top: -20px;
  box-shadow: -10px 19px 38px rgba(83, 83, 83, 0.3),
    10px 15px 12px rgba(80, 80, 80, 0.22);
}

@media screen and (min-width: 320px) and (max-width: 667px) {
  .Movie__Card {
    width: 100%;
  }
}

@media screen and (min-width: 320px) and (max-width: 667px) and (orientation: portrait) {
  .Movie__Card {
    flex-direction: column;
    width: 100%;
  }

  .Movie__Poster {
    width: 100%;
    top: 0;
    left: 0;
  }

  .Movie__Column {
    width: 100% !important;
  }
}
```

<br>

#### CSS (for Loading)

- App.js

```react
render() {
  return (
    <div className={this.state.movieData ? 'App' : 'App--loading'}>
      {this.state.movieData ? this._renderMovies() : 'Loading'}
    </div>
  );
}
```

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m ''
$ git push origin master
```

<br>

<br>