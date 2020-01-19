#### Structure

```bash
src
	├─ index.js
	├─ Table.js
	└─ Column.js
```

<br>

#### index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import Table from './Table';

ReactDOM.render(<Table />, document.getElementById('root'));
```

<br>

#### Table.js

```react
import React, { Component } from 'react';
import Column from './Column';

class Table extends Component {
  render() {
    return (
      <table>
        <tr>
          <Column />
        </tr>
      </table>
    );
  }
}

export default Table;
```

<br>

#### Column.js (div)

```react
import React, { Component } from 'react';

class Column extends Component {
  render() {
    return (
      <div>
        <td>Hello</td>
        <td>World</td>
      </div>
    );
  }
}

export default Column;
```

<br>

- Result:

```html
<div id="root">
  <table>
    <tr>
      <div>
        <td>Hello</td>
        <td>World</td>
      </div>
    </tr>
  </table>
</div>
```

<br>

#### Column.js (React.Fragment)

```react
import React, { Component } from 'react';

class Column extends Component {
  render() {
    return (
      <React.Fragment>
        <td>Hello</td>
        <td>World</td>
      </React.Fragment>
    );
  }
}

export default Column;
```

<br>

- Result:

```html
<div id="root">
  <table>
    <tr>
      <td>Hello</td>
      <td>World</td>
    </tr>
  </table>
</div>
```

<br>

<br>