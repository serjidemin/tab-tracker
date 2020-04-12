<template>
  <panel title="Bookmarks">
    <v-data-table
      :headers="headers"
      :items="bookmarks"
      :items-per-page="5"
      class="elevation-1"
    >
<!--      <template slot="items" >-->

<!--      </template>-->
    </v-data-table>
  </panel>
</template>

<script>
import {mapState} from 'vuex'
import BookmarksService from '../../services/BookmarksService'

export default {
  data () {
    return {
      headers: [
        {
          text: 'Title',
          value: 'title'
        },
        {
          text: 'Artist',
          value: 'artist'
        }
      ],
      bookmarks: []
    }
  },
  computed: {
    ...mapState([
      'isUserLoggedIn',
      'user'
    ])
  },
  async mounted () {
    if (this.isUserLoggedIn) {
      this.bookmarks = (await BookmarksService.index({
        userId: this.user.id
      })).data
    }
  }
}
</script>

<style scoped>
</style>
