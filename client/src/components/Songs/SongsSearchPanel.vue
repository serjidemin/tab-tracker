<template>
  <div class="search">
    <v-text-field
      color="dimgrey"
      v-model="search"
      label="Search by song title, artist, album or genre"
      clearable/>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  data () {
    return {
      search: ''
    }
  },
  watch: {
    search: _.debounce(async function (value) {
      const route = {
        name: 'songs'
      }
      if (this.search !== '') {
        route.query = {
          search: this.search
        }
      }
      this.$router.push(route)
    }, 700),
    '$route.query.search': {
      immediate: true,
      handler (value) {
        this.search = value
      }
    }
  }
}
</script>

<style scoped>
  .search {
    max-width: 500px;
    margin: 0 auto;
  }
</style>
