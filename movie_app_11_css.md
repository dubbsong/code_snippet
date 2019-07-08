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
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
    Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  height: 100%;
  margin: 0;
}

...
```

> `text-align: center;` 제거

<br>

- MovieCard.css

```css
.Movie__Card {
  width: 40%;
  box-shadow: 5px 5px 20px rgba(0, 0, 0, 0.2);
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
  box-shadow: -10px 20px 40px rgba(0, 0, 0, 0.2),
    10px 15px 15px rgba(0, 0, 0, 0.2);
}

.Movie__Genres {
  margin-bottom: 20px;
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
- [x] Add Component
- [x] Set Props
- [x] Set Maping
- [x] Set PropTypes
- [x] Test Lifecycle
- [x] Set State
- [x] Set Stateless Component
- [x] Set AJAX Networking
- [x] Update Component
- [x] Styling CSS
- [] Refactoring
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