<template>
  <div>
  Zaloguj się
  <input type="text" name="login" v-model="user">
  <input type="password" name="password" v-model="password">
    <button v-on:click="handleLogin">submit</button>

        </div>

</template>

<script>
export default {
  name: 'LoginPage',
  data () {
    return {
      password: '',
      user: ''
    }
  },
  methods: {
    handleLogin () {
      let user = this.user
      let password = this.password
      let csrf = this.readCookie('csrftoken')
      this.axios.post('http://localhost:8000/api-auth/login/', user, password, {
        headers: {
          'X-CSRFTOKEN': csrf
        }
      }).then(() => console.log('elo'))
    },
    readCookie (name) {
      let nameEQ = name + '='
      let ca = document.cookie.split(';')
      for (let i = 0; i < ca.length; i++) {
        let c = ca[i]
        while (c.charAt(0) == ' ') c = c.substring(1, c.length)
        if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length, c.length)
      }
      return null
    }
  }
}
</script>
