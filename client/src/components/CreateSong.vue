<template>
  <v-container fluid>
    <v-row dense>
      <v-col cols="4">
        <panel title="Song Metadata">
          <v-text-field
            :rules="[required]"
            v-model="song.title"
            label="Title *"/>

          <v-text-field
            :rules="[required]"
            v-model="song.artist"
            label="Artist *"/>

          <v-text-field
            :rules="[required]"
            v-model="song.genre"
            label="Genre *"/>

          <v-text-field
            :rules="[required]"
            v-model="song.album"
            label="Album *"/>

          <v-text-field
            :rules="[required]"
            v-model="song.albumImageUrl"
            label="Album Image Url *"/>

          <v-text-field
            :rules="[required]"
            v-model="song.youtubeId"
            label="Youtube Id *"/>
        </panel>
      </v-col>

      <v-col cols="8">
        <panel height="400" title="Song Structure">
          <v-textarea
            height="100px"
            :rules="[required]"
            v-model="song.lyrics"
            label="Lyrics *"/>

          <v-textarea
            height="100px"
            :rules="[required]"
            v-model="song.tab"
            label="Tab *"/>
        </panel>
        <div class="error" v-if="error">
          {{ error }}
        </div>
        <v-btn class="ma-2" outlined @click="create">Create</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import SongsService from '@/services/SongsService'

export default {
  data () {
    return {
      song: {
        title: null,
        artist: null,
        genre: null,
        album: null,
        albumImageUrl: null,
        youtubeId: null,
        lyrics: null,
        tab: null
      },
      error: null,
      required: (value) => !!value || 'Required.'
    }
  },
  methods: {
    async create () {
      this.error = null
      const areAllFieldsFilledIn = Object
        .keys(this.song)
        .every(key => !!this.song[key])
      if (!areAllFieldsFilledIn) {
        this.error = 'Please fill in all the required fields.'
        return
      }

      try {
        await SongsService.post(this.song)
        this.$router.push('/songs')
      } catch (e) {
        console.log(e)
      }
    }
  }
}
</script>

<style scoped>
</style>
