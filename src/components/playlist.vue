<template>
  <div class="contents" id="playlist">
    <obg-list ref="list" :scrollbars="$model.options.scrollbars">
      <obg-list-item v-for='(music, index) in musics' @click="changeSource(music, index)" :key="music.info" v-obg-focus>
        <div class='content'>
          <p>{{music.info}}</p>
        </div>
      </obg-list-item>
    </obg-list>
  </div>
</template>

<script>
import {Events} from 'obigo-js-ui'
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
      musics: MUSIC,
      index: 0
    }
  },
  methods: {
    changeSource: function (e, i) {
      let songValue = e.url
      let songImage = e.image
      let songInfo = e.info
      this.index = i
      console.log(songValue, songImage, songInfo, 'playlist changeSource log')
      this.$emit('updateData', [songValue, songImage, songInfo])
      Events.$emit('reload')
    }
  },
  created: function () {
    Events.$on('prev', () => {
      console.log('play prev song')
      if (this.index !== 0) {
        this.index = this.index - 1
        this.$emit('updateData', [MUSIC[this.index].url, MUSIC[this.index].image, MUSIC[this.index].info])
        Events.$emit('reload')
      } else {
        console.log('first song!')
      }
    })
    Events.$on('next', () => {
      console.log('play next song')
      if (this.index + 1 < MUSIC.length) {
        this.index = this.index + 1
        this.$emit('updateData', [MUSIC[this.index].url, MUSIC[this.index].image, MUSIC[this.index].info])
        Events.$emit('reload')
      } else {
        console.log('last song!')
      }
    })
  }
}
</script>
<style scoped>
</style>
