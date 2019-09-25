## Lesson 3: What is Node.js?

###### Node.js는 무엇인가?

- In this lesson, you’ll explore what Node.js is.
  - 이 레슨에서는, Node.js가 무엇인지 살펴본다.
- This includes a brief tour of the V8 JavaScript engine, non-blocking I/O, and more!
  - Node.js에는 V8 JS 엔진, non-blocking I/O 등이 포함된다.
- This lesson contains a presentation that covers what Node.js is.
  - 이 레슨에는 Node.js가 무엇인지 설명하는 프리젠테이션이 포함되어 있다.
- There are no notes for presentation lectures.
  - 프리젠테이션 강의에 대한 노트는 없다.
- Please refer to the video for details.
  - 자세한 내용은 비디오를 참조한다.

<br>

<br>

#### OMB 해석

1. blocking.js

```js
const getUserSync = require('./src/getUserSync')

const userOne = getUserSync(1)
console.log(userOne)

const userTwo = getUserSync(2)
console.log(userTwo)

const sum = 1 + 3
console.log(sum)

// { id: 1, name: 'Sam' }
// { id: 2, name: 'Ralph' }
// 4
```

2. non-blocking.js

```js
const getUser = require('./src/getUser')

getUser(1, (user) => {
  console.log(user)
})

getUser(2, (user) => {
  console.log(user)
})

const sum = 1 + 3
console.log(sum)

// 4
// { id: 1, name: 'Sam' }
// { id: 2, name: 'Ralph' }
```

<br>

<br>

## Lesson 4: Why Should I Use Node.js?

###### Node.js를 사용해야 하는 이유는 무엇인가?

- Why should you use Node.js?
  - 왜 Node.js를 사용해야 하는가?
- In this lesson, you’ll learn what makes Node.js a tool worth using.
  - 이 레슨에서는, 사용할 가치가 있는 Node.js 툴에 대해 학습한다.
- This lesson contains a presentation that covers the major advantages of Node.js.
  - 이 레슨에는 Node.js의 주요 장점을 다루는 프리젠테이션이 포함되어 있다.
- There are no notes for presentation lectures.
  - 프리젠테이션 강의에 대한 메모는 없다.
- Please refer to the video for details.
  - 자세한 내용은 비디오를 참조한다.

<br>

<br>

## Lesson 5: Your First Node.js Script

###### 첫 번째 Node.js 스크립트

- In this lesson, you’ll be creating and running your very first Node.js app.
  - 이 레슨에서는, 첫 번째 Node.js 앱을 생성하고 실행한다.

<br>

#### Creating a Script

###### 스크립트 생성하기

- Node.js scripts are created with the `js` file extension.
  - Node.js 스크립트는 `js` 파일 확장자로 생성된다.
- Remember that Node.js is not a programming language.
  - Node.js는 프로그래밍 언어가 아니다.
- All the code in this course is JavaScript code, which is why the `js` extension is used.
  - 이 코스의 모든 코드는 JS 코드이므로, `js` 확장자가 사용된다.
- Below is an example script stored in a file named `index.js`.
  - 아래 코드는 `index.js`라는 파일에 저장된 예제 스크립트이다.

```js
console.log('Hello NodeJS!')
```

<br>

#### Running a Script

###### 스크립트 실행하기

- You can run a Node.js script using the `node` command.
  - `node` 명령을 사용해서 Node.js 스크립트를 실행할 수 있다.
- Open up a new terminal window and navigate to the directory where the script lives.
  - 새 터미널 창을 열고, 스크립트가 있는 디렉토리로 이동한다.
- From the terminal, you can use the `node` command to provide the path to the script that should run.
  - 터미널에서, `node` 명령을 사용해서 실행할 스크립트의 경로를 제공할 수 있다.
- You can see an example of this command in the terminal below.
  - 아래 터미널에서 명령의 예제를 볼 수 있다.

```bash
$ node index.js
Hello NodeJS!
```

<br>

- When a Node.js script calls `console.log`, the logged values will show up in the terminal.
  - Node.js 스크립트가 `console.log`를 호출하면, 로그된 값이 터미널에 표시된다.
- This is a great way to get output from your Node.js application.
  - 이것이 Node.js 앱에서 출력을 얻는 가장 좋은 방법이다.

<br>

<br>

#### OMB 해석

1. 디렉토리 \& 파일 생성

```bash
$ cd Desktop
$ mkdir test
$ cd test
$ touch index.js
```

2. 코드 작성

```js
// index.js

console.log('Hello NodeJS!')
```

3. 파일 실행

```bash
$ node index.js
Hello NodeJS!
```

<br>

<br>