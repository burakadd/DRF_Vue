<template>
  <div>
      <input v-model="login" type=text placeholder="Login"/>
      <input v-model="password" type=password placeholder="Password"/>
      <button @click="setlogin">Войти</button>
      <br>

  </div>
</template>

<script>
import $ from 'jquery'
export default {
  name: 'Login',
  data () {
    return {
      login: '',
      password: ''
    }
  },
  methods: {
    setlogin () {
      $.ajax({
        url: 'http://127.0.0.1:8000/auth/token/create/',
        type: 'POST',
        data: {
          username: this.login,
          password: this.password
        },
        success: (response) => {
          alert('Hell Yeah')
          sessionStorage.setItem('auth_token', response.data.attributes.auth_token)
          this.$router.push({name: 'homepage'})
        },
        error: (response) => {
          if (response.status === 400) {
            alert('Wrong login or password')
          }
        }

      })
    }
  }
}
</script>

<style scoped>

</style>>
