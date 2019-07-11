- Clock.js

```react
import React, { Component } from 'react';

class Clock extends Component {
  constructor(props) {
    super(props);
    
    this.state = {
      currentTime: new Date()
    };
  }
  
  componentDidMount() {
    setInterval(this.updateTime, 1000);
  }
  
  updateTime = () => {
    this.setState({
      currentTime: new Date()
    });
  };
  
  render() {
    const hours = this.state.currentTime.getHours();
    const minutes = this.state.currentTime.getMinutes();
    const seconds = this.state.currentTime.getSeconds();
    
    return (
      <div className="Clock">
        <h2>
          {hours < 10 ? `0${hours}` : hours} :
          {minutes < 10 ? `0${minutes}` : minutes} :
          {seconds < 10 ? `0${seconds}` : seconds}
        </h2>
      </div>
    );
  }
}
```

<br>

- App.js

```react
import React, { Component } from 'react';
import Clock from './Clock';

class App extends Component {
  render() {
    return (
      <div className="App">
        <Clock />
      </div>
    );
  }
}

export default App;
```

<br>

<br>