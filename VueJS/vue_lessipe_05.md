#### Vuetify

###### 파일 생성

```bash
$ cd src
$ cd components
$ touch User.vue
$ touch UserDetail.vue
$ touch UserEdit.vue
```

<br>

###### 코드 작성

- App.vue

```vue
<template>
  <v-app>
    <v-content>
      <User />
    </v-content>
  </v-app>
</template>

<script>
  import User from './components/User';
  
  export default {
    components: {
      User
    }
  };
</script>
```

- User.vue

```vue
<template>
  <div class="blue lighten-3 pa-3">
    <h1>User 컴포넌트</h1>
    <p>이름: VueJS</p>
    <hr />
    <v-layout row wrap>
      <v-flex xs12 sm6>
        <UserDetail />
      </v-flex>
      <v-flex xs12 sm6>
        <UserEdit />
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
  import UserDetail from './UserDetail';
  import UserEdit from './UserEdit';
  
  export default {
    components: {
      UserDetail,
      UserEdit
    }
  };
</script>
```

- UserDetail.vue

```vue
<template>
  <div class="red lighten-3 pa-3">
    <h3>This is UserDetail</h3>
    <p>Detail</p>
  </div>
</template>
```

- UserEdit.vue

```vue
<template>
  <div class="yellow lighten-3 pa-3">
    <h3>This is UserEdit</h3>
    <p>Edit</p>
  </div>
</template>
```

> 구역별로 표시된다.

<br>

###### 데이터 바인딩

- User.vue

```vue
<template>
  <div class="blue lighten-3 pa-3">
    <h1>User 컴포넌트</h1>
    <p>이름: {{ name }}</p>
    <hr />
    <v-layout row wrap>
      <v-flex xs12 sm6>
        <UserDetail />
      </v-flex>
      <v-flex xs12 sm6>
        <UserEdit />
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
  import UserDetail from './UserDetail';
  import UserEdit from './UserEdit';
  
  export default {
    components: {
      UserDetail,
      UserEdit
    },
    data() {
      return {
        name: "Vuejs"
      }
    }
  };
</script>
```

> 이전과 동일하게 표시된다.

<br>

###### 메소드로 데이터 변경

- User.vue

```vue
<template>
  <div class="blue lighten-3 pa-3">
    <h1>User 컴포넌트</h1>
    <p>이름: {{ name }}</p>
    <button @click="changeName()">CHANGE</button>
    <hr />
    <v-layout row wrap>
      <v-flex xs12 sm6>
        <UserDetail />
      </v-flex>
      <v-flex xs12 sm6>
        <UserEdit />
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
  import UserDetail from './UserDetail';
  import UserEdit from './UserEdit';
  
  export default {
    components: {
      UserDetail,
      UserEdit
    },
    data() {
      return {
        name: "Vuejs"
      }
    },
    methods: {
      changeName() {
        this.name = "ReactJS";
      }
    }
  };
</script>
```

> `CHANGE` 버튼을 클릭하면, `VueJS`가 `ReactJS`로 변경된다.

<br>

###### props 전달

- User.vue

```vue
<template>
  <div class="blue lighten-3 pa-3">
    <h1>User 컴포넌트</h1>
    <p>이름: {{ name }}</p>
    <button @click="changeName()">CHANGE</button>
    <hr />
    <v-layout row wrap>
      <v-flex xs12 sm6>
        <UserDetail :nameOfChild="name" />
      </v-flex>
      <v-flex xs12 sm6>
        <UserEdit />
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
  import UserDetail from './UserDetail';
  import UserEdit from './UserEdit';
  
  export default {
    components: {
      UserDetail,
      UserEdit
    },
    data() {
      return {
        name: "Vuejs"
      }
    },
    methods: {
      changeName() {
        this.name = "ReactJS";
      }
    }
  };
</script>
```

- UserDetail.vue

```vue
<template>
  <div class="red lighten-3 pa-3">
    <h3>This is UserDetail</h3>
    <p>Detail</p>
    <p>{{ nameOfChild }}</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        name
      };
    },
    props: ["nameOfChild"]
  };
</script>
```

> `CHANGE` 버튼을 클릭하면, 두 개의  `VueJS`가 `ReactJS`로 변경된다.

<br>

<br>