#### CSS

- MovieCard.js

```react
<h2>{title}</h2>
```

> title 길이 제한을 제거한다.

<br>

- index.css

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  height: 100%;
  margin: 0;
}

/* html, #root {
  height: 100%;
} */
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
  height: 100%;
}

.App__Loading {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-size: 20px;
}
```

> `text-align: center;` 제거

<br>

- MovieCard.css

```css
.Movie__Card {
  width: 40%;
  /* background-color: #998ac5; */
  box-shadow: 0 8px 38px rgba(133, 133, 133, 0.3),
    0 5px 12px rgba(133, 133, 133, 0.22);
  padding: 0 20px;
  margin-bottom: 50px;
  display: flex;
  justify-content: space-between;
}

.Movie__Card h2 {
  font-size: 20px;
}

.Movie__Column {
  width: 30%;
}

.Movie__Column:last-child {
  width: 60%;
  padding: 20px 0;
}

.Movie__Poster {
  max-width: 100%;
  position: relative;
  top: -20px;
  box-shadow: -10px 19px 38px rgba(83, 83, 83, 0.3),
    10px 15px 12px rgba(80, 80, 80, 0.22);
}

.Movie__Genres {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.Movie__Genre {
  color: #b4b5bd;
  margin-right: 10px;
}

.Movie__Synopsis {
  color: #b4b5bd;
}

@media screen and (min-width: 320px) and (max-width: 667px) {
  .Movie__Card {
    width: 100%;
    flex-direction: column;
    padding-top: 20px;
  }

  .Movie__Column {
    width: 100% !important;
  }

  .Movie__Poster {
    width: 100%;
    top: 0;
    left: 0;
  }
}
```

<br>

#### LinesEllipsis 설치

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

#### LinesEllipsis 추가

- MovieCard.js

```react
...
import LinesEllipsis from 'react-lines-ellipsis';

function MovieCard({ poster, title, genres, synopsis }) {
  return (
    <div className="Movie__Card">
      ...
      <div className="Movie__Column">
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
      </div>
    </div>
  );
}

...
```

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
- [x] Set State
- [x] Set Stateless Component
- [x] Set AJAX Networking
- [x] Update Component
- [x] Styling CSS
- [] Deploying
```

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Styling CSS'
$ git push origin master
```

<br>

<br>