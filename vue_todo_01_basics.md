## 구조

```html
<Root>
  <App>
    <TodoHeader>
    <TodoInput>
    <TodoList>
    <TodoFooter>
```

<br>

<br>

## 기본 설정

#### 프로젝트 생성

```bash
$ cd Desktop
$ vue create vue_todo
```

> `> default (babel, eslint)`를 선택한다.

<br>

#### VSCode 실행

```bash
$ cd vue_todo
$ code .
```

<br>

#### 프로젝트 실행

```bash
$ yarn serve
```

> `http://localhost:8080`에서 프로젝트가 실행된다.

<br>

<br>

#### Google Fonts & FontAwesome 추가

- index.html

```html
<!DOCTYPE html>

<html>
  
  <head>
    ...
    <link href="https://fonts.googleapis.com/css?family=Ubuntu&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.10.1/css/all.css">
    <title>VueJS TODO</title>
  </head>
  
</html>
```

<br>

#### 파일 제거

- src/components/HelloWorld.vue

<br>

#### 컴포넌트 생성

```bash
$ cd src
$ cd components
$ touch TodoHeader.vue
$ touch TodoInput.vue
$ touch TodoList.vue
$ touch TodoFooter.vue
```

<br>

#### 코드 작성

- TodoHeader.vue

```vue
<template>
  <div>
    <p>header</p>
  </div>
</template>

<script>
</script>

<style>
</style>
```

- TodoInput.vue

```vue
<template>
  <div>
    <p>input</p>
  </div>
</template>

<script>
</script>

<style>
</style>
```

- TodoList.vue

```vue
<template>
  <div>
    <p>list</p>
  </div>
</template>

<script>
</script>

<style>
</style>
```

- TodoFooter.vue

```vue
<template>
  <div>
    <p>footer</p>
  </div>
</template>

<script>
</script>

<style>
</style>
```

- App.vue

```vue
<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput></TodoInput>
    <TodoList></TodoList>
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
  import TodoHeader from "./components/TodoHeader";
  import TodoInput from "./components/TodoInput";
  import TodoList from "./components/TodoList";
  import TodoFooter from "./components/TodoFooter";
  
  export default {
    components: {
      TodoHeader: TodoHeader,
      TodoInput: TodoInput,
      TodoList: TodoList,
      TodoFooter: TodoFooter
    }
  };
</script>

<style>
</style>
```

> 화면에 `header`, `input`, `list`, `footer`가 표시된다.

<br>

#### CSS 작성 (Global Style)

- App.vue

```vue
<style>
  body {
    background-color: #f6f6f6;
    text-align: center;
  }
  
  input {
    border-style: groove;
    width: 200px;
  }
  
  button {
    border-style: groove;
  }
  
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
```

<br>

<br>