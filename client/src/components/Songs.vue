<template>
  <panel title="Songs">
    <div v-for="song in songs"
    :key="song.id">
      hello {{ song.artist }}
    </div>
  </panel>
</template>

<script>
import SongsService from '@/services/SongsService'
import Panel from '@/components/Panel'

export default {
  data () {
    return {
      songs: null
    }
  },
  components: {
    Panel
  },
  async mounted () {
    this.songs = (await SongsService.index()).data
  }
}
</script>

<style scoped>
</style>
