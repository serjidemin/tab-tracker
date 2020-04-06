<!--<template>-->
<!--  <v-cotainer>-->
<!--  <v-row>-->
<!--    <v-col-->
<!--      cols="12"-->
<!--      sm="12"-->
<!--      md="6"-->
<!--      class="my-n4">-->
<!--            <v-card  class="mx-6" outlined>-->
<!--              <v-toolbar flat dense  dark>-->
<!--                 <v-toolbar-title>Register</v-toolbar-title>-->
<!--              </v-toolbar>-->

<!--              <div>-->
<!--              <v-text-field-->
<!--                type="email"-->
<!--                name="email"-->
<!--                v-model="email"-->
<!--                label="E-mail"/>-->
<!--              <br>-->
<!--              <v-text-field-->
<!--                type="password"-->
<!--                name="password"-->
<!--                v-model="password"-->
<!--                label="Password"/>-->
<!--              <br>-->
<!--              <div class="error" v-html="error"></div>-->
<!--              <br>-->
<!--              <v-btn class="ma-2" outlined @click="register">Register</v-btn>-->
<!--              </div>-->
<!--            </v-card>-->
<!--          </v-col>-->
<!--        </v-row>-->
<!--        </v-cotainer>-->
<!--</template>-->
<template>
  <v-card flat>
    <v-card
      class="mx-auto"
      max-width="500"
      style="margin-top: 20px;"
    >
      <v-toolbar flat>
        <v-toolbar-title style="color: dimgrey">Register</v-toolbar-title>
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
        <v-btn class="ma-2" outlined @click="register">Register</v-btn>
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
    async register () {
      try {
        await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
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
