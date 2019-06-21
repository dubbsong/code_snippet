#### Basic

```js
function sayHello(name) {
  return 'Hello ' + name;
}

const sam = sayHello('Sam');

console.log(sam);	// Hello Sam
```

<br>

#### Arrow Function

```js
const sayHello = name => 'Hello ' + name;

const sam = sayHello('Sam');

console.log(sam);	// Hello Sam
```

<br>

#### Template Literal

```js
const sayHello = name => `Hello ${name}`;

const sam = sayHello('Sam');

console.log(sam);	// Hello Sam
```

<br>