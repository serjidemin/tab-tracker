<template>
  <v-layot>
    <songs-search-panel />
    <songs-panel />
  </v-layot>
</template>

<script>
import SongsPanel from './SongsPanel'
import SongsSearchPanel from './SongsSearchPanel'
import SongsService from '@/services/SongsService'

export default {
  data () {
    return {
      songs: null
    }
  },
  components: {
    SongsPanel,
    SongsSearchPanel
  },
  async mounted () {
    this.songs = (await SongsService.index()).data
  }
}
</script>

<style scoped>
</style>
