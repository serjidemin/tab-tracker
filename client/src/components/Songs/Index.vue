<template>
  <v-container fluid>
    <v-row dense>
      <v-col cols="5" v-if="isUserLoggedIn">
        <songs-bookmarks/>
        <recently-viewed-songs class="mt-2"/>
      </v-col>
      <v-col cols="7">
        <songs-search-panel />
        <songs-panel />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import SongsPanel from './SongsPanel'
import SongsBookmarks from './SongsBookmarks'
import RecentlyViewedSongs from './RecentlyViewedSongs'
import SongsSearchPanel from './SongsSearchPanel'
import SongsService from '@/services/SongsService'
import {mapState} from 'vuex'

export default {
  data () {
    return {
      songs: null
    }
  },
  computed: {
    ...mapState([
      'isUserLoggedIn'
    ])
  },
  components: {
    SongsPanel,
    SongsSearchPanel,
    SongsBookmarks,
    RecentlyViewedSongs
  },
  async mounted () {
    this.songs = (await SongsService.index()).data
  }
}
</script>

<style scoped>
</style>
