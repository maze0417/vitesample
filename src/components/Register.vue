<template>
  <div class="container">
    <form @submit.prevent="register">
      <input class="input-field" v-model="email" placeholder="Email">
      <input class="input-field" v-model="password" type="password" placeholder="Password">
      <input class="input-field" v-model="captcha" placeholder="Captcha">
      <button class="submit-button" type="submit">Register</button>
    </form>
  </div>
</template>

<script>
import { ref } from 'vue';
import axios from 'axios';

export default {
  setup() {
    const email = ref('');
    const password = ref('');
    const captcha = ref('');

    const register = async () => {
      try {
        const response = await axios({
          method: 'post',
          url: 'http://fnb238.com/index.php?r=demo/registerA',
          headers: {
            'Content-Type': 'application/json',
            'Cookie': 'PHPSESSID=3i7ghdck1ngp6udlmrjf411f12', // Usually, cookies are handled automatically by the browser
            'Email': email.value,
          },
          data: {
            "Email": email.value,
            "Password": password.value,
            "Captcha": captcha.value
          }
        });

        alert(response.msg)

        console.log(response);
      } catch (error) {
        console.error(error);
      }
    };

    return {
      email,
      password,
      captcha,
      register,
    };
  },
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 10px;
}

.input-field {
  display: block;
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  box-sizing: border-box;
}

.submit-button {
  display: block;
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
}
</style>