#### Spread Operator

1. array

```js
const days = ['Sun', 'Mon', 'Tue'];
const otherDays = ['Wed', 'Thu', 'Fri'];
let allDays = [...days, otherDays, 'Sat'];

console.log(allDays);	// ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']
```

<br>

2. obejct

```js
const obj1 = {
  firstName: 'Sam',
  lastName: 'Azor'
};

const obj2 = {
  age: 28,
  nationality: 'Aussie'
};

const sum = { ...obj1, ...obj2 };

console.log(sum);	// { firstName: 'Sam', lastName: 'Azor', age: 28, nationality: 'Aussie' }
```

<br>