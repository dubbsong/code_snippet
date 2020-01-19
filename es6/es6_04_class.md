#### Class

1. basic

```js
class Human {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}

const sam = new Human('Coco', 'Song');

console.log(sam);	// Human { firstName: 'Coco', lastName: 'Song' }
console.log(sam.firstName);	// Coco
```

<br>

2. extends

```js
class Human {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}

class Baby extends Human {
  cry() {
    console.log('Wooooaaaa');
  }
}

const myBaby = new Baby('mini', 'me');

console.log(myBaby);	// Baby { firstName: 'mini', lastName: 'me' }
console.log(myBaby.cry());	// Wooooaaaa
```

<br>