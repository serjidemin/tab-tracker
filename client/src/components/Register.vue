<template>
  <panel title="Register">
    <v-text-field
      type="email"
      name="email"
      v-model="email"
      label="E-mail"/>
    <br>
    <v-text-field
      type="password"
      name="password"
      v-model="password"
      label="Password"/>
    <br>
    <div class="error" v-html="error"></div>
    <br>
        <v-btn class="ma-2" outlined @click="register">Register</v-btn>
  </panel>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
import Panel from '@/components/Panel'

export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
      } catch (e) {
        this.error = e.response.data.error
      }
    }
  },
  components: {
    Panel
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .error {
    color: white;
  }
</style>
