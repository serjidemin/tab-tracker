<template>
  <panel maxWidth="500" title="Songs">
    <template v-slot:extension>
      <v-btn
        color="light-blue darken-2"
        dark
        small
        absolute
        right
        fab
        to="/songs/create"
      >
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </template>
    <div v-for="song in songs"
    :key="song.id">
      <v-container fluid>
        <v-row dense>
          <v-col cols="6">
            <div class="song-title">
              {{ song.title }}
            </div>
            <div class="song-artist">
              {{ song.artist }}
            </div>
            <div class="song-genre">
              {{ song.genre }}
            </div>

            <v-btn
              class="ma-2"
              outlined
              @click="navigateTo({
                name: 'song',
                params: {
                  songId: song.id
                }
              })">
              View
            </v-btn>
          </v-col>

          <v-col cols="6">
            <img class="album-image" :src="song.albumImageUrl" />
          </v-col>
        </v-row>
      </v-container>
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
  methods: {
    navigateTo (route) {
      this.$router.push(route)
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
  .song-title {
    font-size: 30px;
  }

  .song-artist {
    font-size: 24px;
  }

  .song-genre {
    font-size: 18px;
  }

  .album-image {
    width: 70%;
    margin: 0 auto;
  }
</style>
