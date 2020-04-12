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

        <v-btn
          v-if="isUserLoggedIn && !bookmark"
          class="ma-2"
          outlined
          @click="setAsBookmark"
          >
          Set As Bookmark
        </v-btn>

        <v-btn
          v-if="isUserLoggedIn && bookmark"
          class="ma-2"
          outlined
          @click="unsetAsBookmark"
        >
          Unset As Bookmark
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
import { mapState } from 'vuex'
import BookmarksService from '@/services/BookmarksService'

export default {
  props: [
    'song'
  ],
  data () {
    return {
      bookmark: null
    }
  },
  computed: {
    ...mapState([
      'isUserLoggedIn',
      'user'
    ])
  },
  watch: {
    async song () {
      if (!this.isUserLoggedIn) {
        return
      }

      try {
        const bookmarks = (await BookmarksService.index({
          songId: this.$store.state.route.params.songId,
          userId: this.user.id
        })).data
        if (bookmarks.length) {
          this.bookmark = bookmarks[0]
        }
      } catch (e) {
        console.log(e)
      }
    }
  },
  methods: {
    async setAsBookmark () {
      try {
        this.bookmark = (await BookmarksService.post({
          songId: this.$store.state.route.params.songId,
          userId: this.user.id
        })).data
      } catch (e) {
        console.log(e)
      }
    },
    async unsetAsBookmark () {
      try {
        await BookmarksService.delete(this.bookmark.id)
        this.bookmark = null
      } catch (e) {
        console.log(e)
      }
    }
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
