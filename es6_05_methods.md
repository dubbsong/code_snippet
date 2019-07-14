#### map

```js
const days = ['Sun', 'Mon', 'Tue'];

const addNum = days.map((day, index) => `#${index + 1} ${day}`);

console.log(addNum);	// ['#1 Sun', '#2 Mon', '#3 Tue']
```

> `map()` 메소드
>
> 배열 내 모든 element에 대해, 호출한 함수의 결과를 모아 새 배열로 반환한다.

<br>

#### filter

```js
const nums = [4, 28, 44, 4, 36, 21];

const biggerThan25 = nums.filter(num => num > 25);

console.log(biggerThan25);	// [28, 44, 36]
```

> `filter()` 메소드
>
> 테스트를 통과한 배열의 각 값을 모아, 새 배열로 반환한다.

<br>

#### forEach

```js
const sayHello = ['Hi', 'How are you?', 'All good?'];

sayHello.forEach(i => console.log(i));

// Hi
// How are you?
// All good?
```

> `forEach()` 메소드
>
> 배열의 각 element에 대해, 제공된 함수를 차례로 한 번씩 호출한다.

<br>

#### push

```js
const days = ['Sun', 'Mon', 'Tue'];

days.push('Wed');

console.log(days);	// ['Sun', 'Mon', 'Tue', 'Wed']
```

> `push()` 메소드
>
> 배열의 끝에 새 element를 추가하고, 새로운 길이를 반환한다.

<br>

#### includes

```js
const days = ['Sun', 'Mon', 'Tue'];

if (!days.includes('Wed')) {
  days.push('Wed');
}

console.log(days);	// ['Sun', 'Mon', 'Tue', 'Wed']
```

> `includes()` 메소드
>
> 특정 값이 있는지 확인하고, true/false를 반환한다.

<br>