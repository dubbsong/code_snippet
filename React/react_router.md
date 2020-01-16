#### 구조

```bash
src
	├─ Component
	│		├─ App.js
	│		├─ Header.js
	│		└─ Router.js
	├─ Routes
	│		├─ Home.js
	│		├─ TV.js
	│		├─ Search.js
	│		└─ Detail.js
	└─ index.js
```

<br>

#### react-router-dom 설치

```bash
$ yarn add react-router-dom
```

<br>

#### App.js

```react
import React, { Component } from 'react';
import Router from 'Components/Router';

class App extends Component {
  render() {
    return (
      <>
      	<Header />
        <Router />
      </>
    );
  }
}

export default App;
```

<br>

#### Router.js

```react
import React from 'react';
import { BrowserRouter as Router, Route } from 'react-router-dom';
import Home from 'Routes/Home';
import TV from 'Routes/TV';
import Search from 'Routes/Search';

export default () => (
  <Router>
    <>
      <Route path="/" exact component={Home} />
      <Route path="/tv" component={TV} />
      <Route path="/tv/popular" render={() => <h2>Popular</h2>} />
      <Route path="/search" component={Search} />
    </>
  </Router>
);
```

<br>

#### Home.js

```react
export default () => 'Home';
```

<br>

#### TV.js

```react
export default () => 'TV';
```

<br>

#### Search.js

```react
export default () => 'Search';
```

<br>

#### Detail.js

```react
export default () => 'Detail';
```

------

<br>

#### Header.js

```react
import React from 'react';

export default () => (
  <header>
    <ul>
      <li>
        <a href="/">Movies</a>
      </li>
      <li>
        <a href="/tv">TV</a>
      </li>
      <li>
        <a href="/search">Search</a>
      </li>
    </ul>
  </header>
);
```

<br>

#### Router.js

```react
import React from 'react';
import { BrowserRouter as Router, Route, Redirect, Switch } from 'react-router-dom';
import Home from 'Routes/Home';
import TV from 'Routes/TV';
import Search from 'Routes/Search';

export default () => (
  <Router>
    <Switch>
      <Route path="/" exact component={Home} />
      <Route path="/tv" component={TV} />
      <Route path="/search" component={Search} />
      <Redirect from="*" to="/" />
    </Switch>
  </Router>
);
```

<br>

#### Check

> `localhost:3000`: Home
>
> `localhost:3000/tv`: TV
>
> `localhost:3000/tv/popular`: TV Popular
>
> `localhost:3000/search`: Search
>
> `localhost:3000` 뒤에 `/asdfjlas;df`와 같이 아무거나 입력해도, Home으로 Redirect 한다.

<br>