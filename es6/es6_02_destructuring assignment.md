#### Destructuring Assignment (구조 분해 할당)

```js
const human = {
  firstName: 'Sam',
  lastName: 'Azor',
  nationality: 'Australia',
  favFood: {
    breakfast: 'Mcmorning',
    lunch: 'Sandwich',
    dinner: 'Pork belly'
  }
};

const firstName = human.firstName;
const lastName = human.lastName;
console.log(firstName, lastName); // Sam Azor

// 구조 분해 할당
const { nationality: difName } = human;
const {
  favFood: { dinner }
} = human;

console.log(difName); // Australia
console.log(dinner); // Pork belly
```

<br>

<br>