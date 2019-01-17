<template>
  <v-layout column>
    <v-flex xs3 offset-xs3>
      <panel title="Register">
        <form
          name="tab-tracker-form"
          autocomplete="off">
          <v-text-field
            label="Email"
            v-model="email"
          ></v-text-field>
          <br>
          <v-text-field
            label="Password"
            type="password"
            v-model="password"
            autocomplete="new-password"
          ></v-text-field>
        </form>
        <br>
        <div class="danger-alert" v-html="error" />
        <br>
        <v-btn
          dark
          class="blue"
          @click="register">
          Register
        </v-btn>
      </panel>
    </v-flex>
  </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  watch: {
    email (value) {
      console.log('email has changed: ', value)
    }
  },
  mounted () {
    setTimeout(() => {
      // this.email = 'heloooooo2000'
    }, 2000)
  },
  methods: {
    async register () {
      try {
        const resp = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        this.error = 'Register OK: ' + resp.data.user.email
        this.$store.dispatch('setToken', resp.data.token)
        this.$store.dispatch('setUser', resp.data.user)
        this.$router.push({
          name: 'songs'
        })
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
