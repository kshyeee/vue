<template>
  <!-- <form action="" @submit.prevent="submitForm"> :::: .prevent <= 컴포넌트 안의 methods에 event.preventDefault 의 이벤트트 직접 템플릿 표현식으로 지정할수있다. -->
  <form action="" @submit.prevent="submitForm">
    <div>
      <label for="userId">ID:</label>
      <input id="userId" type="text" v-model="username">
    </div>
    <div>
      <label for="password">PW:</label>
      <input id="" type="text" v-model="password">
    </div>
    <button type="submit">로그인</button>
  </form>
</template>

<script>
  import axios from 'axios' // 1.axios 설치, 2.package.json에 보면 dependencies > 에 axios 설치된 거 확인
  import { ref } from 'vue';

  export default {
    setup() {
      // dara
      var username = ref('');
      var password = ref('');

      // methods
      var submitForm = () => {
        axios.post('https://jsonplaceholder.typicode.com/users/', {
          username: username.value,
          password: password.value
        }).then(response => {
          console.log(response);
        })
      }

      return { username, password, submitForm }
    },
    // data() {
    //   return {
    //     username: '',
    //     password: '',
    //   }
    // },
    // methods: {
    //   submitForm() {
    //     const data = {
    //       username: this.username,
    //       password: this.password,
    //     }
    //     axios.post('https://jsonplaceholder.typicode.com/users/', data)
    //     .then(response => {
    //       console.log(response)
    //     });
    //     //console.log('제출됨');
    //   }
    //   // submitForm(event) {
    //   //   // event.preventDefault(); // 이벤트를 받아서 폼의 기본적인 동작을 막기 위해 preventDefault를 이용. (페이지에서 새로고침 하면 폼 작성했던게 날라가지않기 위해)
    //   //   console.log('제출됨');
    //   // }
    // }
  }
</script>

<style scoped>

</style>