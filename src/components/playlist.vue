<template>
  <div class="contents" id="playlist">
    <obg-list ref="list" :scrollbars="$model.options.scrollbars">
      <obg-list-item v-for='(music, index) in musics' @click="changeSource(music)" :key="music.info" v-obg-focus>
        <div class='content'>
          <p>{{music.info}}</p>
        </div>
      </obg-list-item>
    </obg-list>
  </div>
</template>

<script>
import { bus } from '../main'
import {list, listItem} from 'obigo-js-ui-rnbs/components/list'
import {MUSIC} from './music-list'
export default {
  name: 'playlist',
  components: {
    'obg-list': list,
    'obg-list-item': listItem
  },
  props: {
    currentSong: {
      type: String
    },
    currentImage: {
      type: String
    },
    currentInfo: {
      type: String
    }
  },
  data () {
    return {
      musics: MUSIC
    }
  },
  methods: {
    changeSource: function (e) {
      let songValue = e.url
      let songImage = e.image
      let songInfo = e.info
      console.log(songValue, songImage, songInfo, 'playlist changeSource log')
      this.$emit('updateData', [songValue, songImage, songInfo])
      bus.$emit('reload')
    }
  }
}
</script>
<style scoped>
</style>
