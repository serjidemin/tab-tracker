<template>
  <div>
    <v-app-bar
      color="blue lighten-3"
      dense
      dark
      fixed
    >
<!--      <v-app-bar-nav-icon></v-app-bar-nav-icon>-->

      <v-toolbar-title>
        <router-link
          tag="span"
          class="home"
          :to="{name: 'songs'}">
          TabTracker
        </router-link>
      </v-toolbar-title>

      <v-toolbar-items style="margin-left: 10px">
        <v-btn
          color="blue lighten-3"
          depressed
          :to="{name: 'songs'}">
            <v-icon left>mdi-folder-open</v-icon>
          BROWSE
        </v-btn>
      </v-toolbar-items>

      <v-spacer></v-spacer>
            <v-toolbar-items v-if="!$store.state.isUserLoggedIn">
              <v-btn
                color="blue lighten-3"
                depressed
                :to="{name: 'login'}">
                <v-icon left>mdi-account</v-icon>
                Sign IN
              </v-btn>
            </v-toolbar-items>

            <v-toolbar-items v-if="!$store.state.isUserLoggedIn">
              <v-btn
                color="blue lighten-3"
                depressed
                :to="{name: 'register'}">
                <v-icon left>mdi-account-plus</v-icon>
                Sign UP
              </v-btn>
            </v-toolbar-items>

      <v-toolbar-items v-if="$store.state.isUserLoggedIn">
        <v-menu
          left
          bottom>
          <template v-slot:activator="{ on }">
            <v-btn
              color="blue lighten-3"
              depressed
              v-on="on">
              {{ $store.state.user.email }}
              <v-icon>mdi-dots-vertical</v-icon>
            </v-btn>
          </template>

          <v-list>
            <v-list-item
              @click="() => {}"
            >
              <v-list-item-title>Option 1</v-list-item-title>
            </v-list-item>
            <v-list-item
              @click="logout"
            >
              <v-list-item-title>
                <v-icon left color="black">mdi-logout</v-icon>
                Log Out
              </v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-toolbar-items>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  methods: {
    logout () {
      this.$store.dispatch('setToken', null)
      this.$store.dispatch('setUser', null)
      this.$router.push({
        name: 'songs'
      })
    }
  }
}
</script>

<style scoped>
  .home {
    cursor: pointer;
  }

</style>
