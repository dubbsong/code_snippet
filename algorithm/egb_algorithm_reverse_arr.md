#### Problem

- 배열의 각 item을 거꾸로 나열해서 반환한다.

<br>

#### Solution 01

```js
function reverse(arr) {
  let resut = [];
  
  for (let i = arr.length - 1; i >= 0; i--) {
    result.push(arr[i]);
  }
  return result;
}

reverse([1, 2, 3, 4]);  // [4, 3, 2, 1]
reverse([4, 3, 2, 1]);  // [1, 2, 3, 4]
```

<br>

#### Solution 02

```js
function reverse(arr) {
  return arr.toString().split(',').reverse().map(i => parseInt(i));
}

reverse([1, 2, 3, 4]);  // [4, 3, 2, 1]
reverse([4, 3, 2, 1]);  // [1, 2, 3, 4]
```

<br>

#### Solution 03

```js
function reverse(arr) {
  return arr.toString().split(',').reverse().map(Number);
}

reverse([1, 2, 3, 4]);  // [4, 3, 2, 1]
reverse([4, 3, 2, 1]);  // [1, 2, 3, 4]
```

<br>

#### Solution 04

```js
function reverse(arr) {
  return (arr + '').split(',').reverse().map(Number);
}

reverse([1, 2, 3, 4]);  // [4, 3, 2, 1]
reverse([4, 3, 2, 1]);  // [1, 2, 3, 4]
```

<br>

#### Solution from 팀장님

```js
function reverse(arr) {
  for (let i = 0; i < arr.length / 2; i++) {
    let temp = arr[i];
    arr[i] = arr[arr.length - i - 1];
    arr[arr.length - i - 1] = temp;
  }
  return arr;
}

reverse([1, 2, 3, 4]);  // [4, 3, 2, 1]
reverse([4, 3, 2, 1]);  // [1, 2, 3, 4]
```

<br>

<br>