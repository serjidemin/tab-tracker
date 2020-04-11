<template>
  <panel title="Song Metadata">
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
          :to="{
                name: 'song-edit',
                params () {
                  return {
                    songId: song.id
                  }
                }
              }">
          Edit
        </v-btn>
      </v-col>

      <v-col cols="6">
        <img class="album-image" :src="song.albumImageUrl" />
        <br>
        {{ song.album }}
      </v-col>
    </v-row>
  </panel>
</template>

<script>
export default {
  props: [
    'song'
  ]
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
