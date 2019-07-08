#### Refactoring

- MovieCard.js

```react
...

function MovieCard({ ... }) {
  return (
    <div className="Movie__Card">
      ...
      <div className="Movie__Column">
        ...
        <div className="Movie__Genres">
          {genres.map((genre, index) => (
            <MovieGenre genre={genre} key={index} />
          ))}
        </div>
        ...
      </div>
    </div>
  );
}

function MovieGenre({ genre }) {
  return <span className="Movie__Genre">{genre}</span>;
}

MovieCard.propTypes = {
  ...
};

MovieGenre.propTypes = {
  genre: PropTypes.string.isRequired
};

...
```

<br>

- MovieCard.css

```css
...

.Movie__Genres {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.Movie__Genre {
  color: #b4b5bd;
  margin-right: 10px;
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
- [x] Refactoring
- [] Deploying
```

<br>

#### Commit

```bash
$ cd movie_app
$ git status
$ git add .
$ git commit -m 'Refactoring'
$ git push origin master
```

<br>

<br>