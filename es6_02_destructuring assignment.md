#### Inefficient

```js
const human = {
  name: 'Sam',
  lastName: 'Azor',
  nationality: 'Australia'
}

const name = human.name;
const lastName = human.lastName;

console.log(name, lastName);	// Sam Azor
```

<br>

#### Destructuring Assignment

- 더 적은 코드를 사용해서 좀 더 깔끔하게 보이게 한다.

```js
const human = {
  name: 'Sam',
  lastName: 'Azor',
  nationality: 'Australia',
  favFood: {
    breakfast: 'Mcmorning',
    lunch: 'Subway',
    dinner: 'pork belly'
  }
}

const { nationality: differentName } = human;
const { favFood: { dinner }} = human;

console.log(differentName);	// Australia
console.log(dinner);	// pork belly
```

<br>