<template>
  <v-layout column>
    <v-flex xs3 offset-xs3>
      <panel title="Songs">
        <!--
        <h3> aaabbbbbbbbbbccccccccccc</h3>
        <p>
          hhhhheeeeeeeeeeeeeeeeee
        </p>
        -->
        <v-btn
          @click="navigateTo({name: 'songs-create'})"
          slot="action"
          class="blue accent-2"
          dark
          medium
          absolute
          right
          middle
          fab>
          <v-icon>add</v-icon>
        </v-btn>
        <div
          v-for="song in songs"
          :key="song.id">

          <v-layout>
            <v-flex xs6>
              <div class="song-title">
                {{song.title}}
              </div>
              <div class="song-artist">
                {{song.artist}}
              </div>
              <div class="song-genre">
                {{song.genre}}
              </div>

              <v-btn
                dark
                class="blue"
                @click="navigateTo({
                  name: 'song',
                  params: {
                    songId: song.id
                  }
                })">
                View
              </v-btn>
            </v-flex>
            <v-flex xs6>
              <img class="album-image" :src="song.albumImageUrl" />
            </v-flex>
          </v-layout>
        </div>
       </panel>
    </v-flex>
  </v-layout>
</template>

<script>
import SongsService from '@/services/SongsService'
import Panel from '@/components/globals/Panel'
export default {
  components: {
    Panel
  },
  data () {
    return {
      error: '<label> aaa </label>',
      songs: null
      /*
      songs: [
        {
        title: 'Hello',
        artist: 'aaa',
        album: 'bbb'
      }
      ]
  */
    }
  },
  methods: {
    async navigateTo (route) {
      this.$router.push(route)
    }
  },
  async mounted () {
    this.songs = (await SongsService.index()).data
  }
}
</script>

<style scoped>
.song {
  padding: 20px;
  height: 330px;
  overflow: hidden;
}

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
