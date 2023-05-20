<template>
  <div class="login">
    <div class="login-wrapper">
      <div class="title">Vote System</div>
      <LoginForm :method="userLogin" v-on:login="login"></LoginForm>
    </div>
  </div>
</template>

<script>
import LoginForm from '@/components/LoginForm.vue'
export default {
  name: 'LoginComponent',
  components: {
    LoginForm
  },
  data() {
    return {
      userLogin: {
        title: 'Login to Vote',
        type: 'userLogin'
      },
      managerLogin: {
        title: 'Manager Login',
        type: 'managerLogin'
      }
    }
  },
  methods: {
    async login({username, password}) {
      console.log('url', `${process.env.VUE_APP_BACKEND_URL}/api/login`);
      try {
        const {status} = await fetch(`${process.env.VUE_APP_BACKEND_URL}/api/login`, {
          method: 'POST',
          body: JSON.stringify({
            name: username,
            password: password
          }),
          headers: {
            'Content-Type': 'application/json'
          }
        })
        if(status === 200) {
          this.$router.push('/vote');
        } else {
          alert('輸入內容錯誤，請重新輸入');
        }
      } catch(err){
        console.log(err);
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.login {
  width: 100%;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.title {
  font-size: 64px;
  font-weight:900;
  color: #416586;
  margin-bottom: 20px;
}
</style>
