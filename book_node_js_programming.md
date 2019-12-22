## Node.js 프로그래밍

###### 정민석 지음

<br>

<br>

#### CH01 인터넷과 웹

- 웹을 구성하는 가장 중요한 두 요소로 `웹 브라우저`와 `웹 서버`를 꼽을 수 있다.
- Chrome은 `Webkit 엔진`을 사용하여 화면을 구성하고, `V8 엔진`을 사용하여 JS를 해석한다.
- Chrome을 지탱하는 가장 큰 엔진은, `Blink`라고 불리는 렌더링 엔진과 `V8`이라고 불리는 JS 해석 엔진이다.
- Node.js는 JS를 구동하는 V8 엔진으로만 구성되어 있다.

<br>

<br>

#### CH02 Node.js의 특징과 장단점

- JS는 기본적으로 이벤트를 처리하는 데 강점을 보인다. 순차적으로 실행되는 것이 아니라, 중간중간 이벤트 발생 시 해당 이벤트를 그때그때 처리하는 데 강하다는 의미이다.
- 동기식은 해야 할 작업을 모두 순서대로 처리한다. 외부에서 특정 URL을 요청하는 경우, 해당 페이지를 보여주기 위해 1) 파일을 읽어서 2) 해당 파일에 있는 내용에 따라 DB에서 데이터를 읽어 오고 3) 몇 가지 계산을 처리한 뒤 사용자에게 반환하는 프로세스이다. 말 그대로 순서대로 처리한다. 여러 명의 요청이 들어오면 여러 프로세스를 동시에 처리하는 식이다.
- 비동기식 혹은 Event Driven은 하나의 프로세스가 모든 것을 동시에 처리하지만, 그때그때 처리한다. 1) 요청이 오면 파일 읽기를 시작하고, 파일을 불러오는 동안 기다린다. 2) 그동안 요청이 오면 또 파일 읽기를 시도한다. 역시 읽기가 끝날 때까지 다른 일을 하면서 기다린다. 1)의 요청에 대한 읽기가 끝났다고 `이벤트`가 발생하면, 그때 DB에서 데이터를 요청한다. 이 역시 시간이 걸리는 작업이므로, 이벤트가 발생할 때까지 다른 일을 하면서 기다린다. 그 후 데이터가 왔다는 이벤트가 발생하면, 마지막으로 계산하고 요청에 응답한다. 즉, 외부에서 이벤트가 발생할 때마다 해당 이벤트 위주로 처리를 한다고 보면 된다. 이러한 처리 방식을 `Event Driven` 방식이라고 한다.
- Node.js는 한 개의 코어밖에 사용하지 못한다. 이러한 것을 싱글 스레드로 돌아간다고 한다.
- Node.js는 Event Driven 시스템이고, 최고의 효율을 위해 멀티 스레드로 돌리면 되지만, 멀티 스레드는 손이 매우 많이 가는 방법이다. 클러스터(cluster) 간 메모리 공유도 안 되고, 몇 가지 처리르 할 때는 주의할 점도 많다.

<br>

<br>

#### CH03 개발을 위한 사전 준비

- Node.js는 기본적으로 서버를 위한 언어이다. 따라서 서버(프로그램 의미의)를 만들기 위해 서버(하드웨어 의미의)가 있어야 한다.

<br>

###### Node.js 버전 확인

```bash
$ node -v
```

<br>

###### 처음으로 구동하는 Node.js 서버

- test.js

```js
const http = require('http');

const port = 80;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, (err) => {
  if (err) {
    console.log(err);
  }
  console.log(`Server running`);
});
```

> `$ node test.js`를 입력하면, `127.0.0.1`에서 `Hello World`를 확인할 수 있다.

- 일반 사용자 계정은 `$`로 시작하고, 관리자 계정은 `#`으로 시작한다.
- 만약 그렇지 않다면, `$sudo su`를 통해 관리자 권한으로 전환한다.

<br>

<br>

#### CH04 Hello World

- test.js

```js
const http = require('http');
const port = 80;
const hostname = '127.0.0.1';

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, (err) => {
  if (err) {
    console.log(err);
  }
  console.log(`Server running`);
});
```

- 첫 번째 줄은 http라는 모듈을 불러오는 부분이다.
- http 서비스를 하는 경우에는 일반적으로 80 포트를, https 서비스의 경우에는 443 포트로 설정한다.
- Listen은 실제로 서버 모듈을 동작하도록 `실행`하는 부분이다.
- createServer는 실행을 하기 전 어떤 식으로 동작해야 할지 `선언`하는 부분이다.
- Header는 눈에 보이지 않지만, 하는 일이 매우 중요하다. 상당히 중요한 많은 정보를 표시하기 때문이다.

<br>

- test.js

```js
const http = require('http');
const server = http.createServer((req, res) => {
  var ip = req.headers['x-forwarded-for'] || req.connection.remoteAddress;
  console.log("ip: ", ip);
  console.log("url: ", req.url);
  console.log("headers: ", req.headers);
  
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n' + JSON.stringify(req.headers, null, 4));
});

server.listen(80, (err) => {
  if (err) {
    console.log(err);
  }
  console.log(`Server running`);
});
```

- `node test.js`

```json
{
  "host": "127.0.0.1",
  "connection": "keep-alive",
  "cache-control": "max-age=0",
  "upgrade-insecure-requests": "1",
  "user-agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_1) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.79 Safari/537.36",
  "sec-fetch-user": "?1",
  "accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
  "sec-fetch-site": "none",
  "sec-fetch-mode": "navigate",
  "accept-encoding": "gzip, deflate, br",
  "accept-language": "ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7"
}
```

- 실제로 동작하는 표준 코드 정도로 이해하면 된다.

<br>

<br>

#### CH05 Node.js 시작하기

- 디버깅하는 가장 기본적인 방법은, 화면에 현재 프로그램의 상태를 출력하는 것이다.
- test.js

```js
setIntervel(() => {
  console.log('Now Time is ', new Date());
}, 5 * 1000);
```

> `$ node test.js`
>
> 현재 시간을 Terminal에 5초마다 출력한다.

<br>

<br>