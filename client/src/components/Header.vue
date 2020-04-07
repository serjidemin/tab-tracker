<template>
  <div>
    <v-app-bar
      color="blue lighten-3"
      dense
      dark
    >
<!--      <v-app-bar-nav-icon></v-app-bar-nav-icon>-->

      <v-toolbar-title>
        <span class="home" @click="navigateTo({name: 'root'})">
          TabTracker
        </span>
      </v-toolbar-title>

<!--      TODO: Implement Me-->
<!--      <v-toolbar-items style="margin-left: 10px">-->
<!--        <v-btn color="blue lighten-3"-->
<!--               depressed>-->
<!--          <v-icon left>mdi-folder-open</v-icon>-->
<!--          BROWSE-->
<!--        </v-btn>-->
<!--      </v-toolbar-items>-->

      <v-spacer></v-spacer>
            <v-toolbar-items>
              <v-btn
                v-if="!$store.state.isUserLoggedIn"
                color="blue lighten-3"
                depressed
                to="login">
                <v-icon left>mdi-account</v-icon>
                Sign IN
              </v-btn>
            </v-toolbar-items>

            <v-toolbar-items>
              <v-btn
                v-if="!$store.state.isUserLoggedIn"
                color="blue lighten-3"
                depressed
                to="register">
                <v-icon left>mdi-account-plus</v-icon>
                Sign UP
              </v-btn>
            </v-toolbar-items>

      <v-toolbar-title v-if="$store.state.isUserLoggedIn">
          {{ $store.state.user.email }}
      </v-toolbar-title>

      <v-menu
        left
        bottom
        v-if="$store.state.isUserLoggedIn">
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item
            v-for="n in 3"
            :key="n"
            @click="() => {}"
          >
            <v-list-item-title>Option {{ n }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  }
}
</script>

<style scoped>
  .home {
    cursor: pointer;
  }

</style>
