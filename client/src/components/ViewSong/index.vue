<template>
    <v-container fluid>
      <v-row dense>
        <v-col cols="6">
          <song-metadata :song="song"/>
        </v-col>
        <v-col cols="6">
          <youtube :youtubeId="song.youtubeId"/>
        </v-col>
      </v-row>

      <v-row dense>
        <v-col cols="6">
          <tab :tab="song.tab"/>
        </v-col>
        <v-col cols="6">
          <lyrics :lyrics="song.lyrics"/>
        </v-col>
      </v-row>
    </v-container>
</template>

<script>
import SongsService from '@/services/SongsService'
import Youtube from '@/components/ViewSong/YouTube'
import Lyrics from '@/components/ViewSong/Lyrics'
import Tab from '@/components/ViewSong/Tab'
import SongMetadata from '@/components/ViewSong/SongMetadata'

export default {
  data () {
    return {
      song: {}
    }
  },
  async mounted () {
    const songId = this.$store.state.route.params.songId
    this.song = (await SongsService.show(songId)).data
  },
  components: {
    SongMetadata,
    Youtube,
    Lyrics,
    Tab
  }
}
</script>

<style scoped>
</style>
