<template>
  <v-card flat>
    <v-card
      class="mx-auto"
      max-width="500"
      style="margin-top: 20px;"
    >
      <v-toolbar flat>
        <v-toolbar-title style="color: dimgrey">Login</v-toolbar-title>
      </v-toolbar>
      <v-divider></v-divider>
      <v-card-text>
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
        <v-btn class="ma-2" outlined @click="login">Login</v-btn>
      </v-card-text>
    </v-card>
  </v-card>
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
  methods: {
    async login () {
      try {
        const response = await AuthenticationService.login({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
      } catch (e) {
        this.error = e.response.data.error
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.error {
  color: white;
}
</style>
