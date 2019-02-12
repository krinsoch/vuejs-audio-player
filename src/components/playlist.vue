<template>
  <div class="contents" id="playlist">
    <obg-list ref="list" :scrollbars="$model.options.scrollbars">
      <obg-list-item v-for='(music, index) in musics' @click="selectSource(index)" :key="music.info" v-obg-focus>
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
    selectSource: function (i) {
      this.index = i
      console.log('select song: ' + MUSIC[i].info)
      this.changeSource(i)
    },
    changeSource: function (i) {
      this.$emit('updateData', [MUSIC[i].url, MUSIC[i].image, MUSIC[i].info])
      Events.$emit('reload')
    }
  },
  created: function () {
    Events.$on('prev', () => {
      console.log('play prev song')
      if (this.index !== 0) {
        this.index = this.index - 1
        this.changeSource(this.index)
      } else {
        console.log('first song!')
        this.index = MUSIC.length - 1
        this.changeSource(this.index)
      }
    })
    Events.$on('next', () => {
      console.log('play next song')
      if (this.index + 1 < MUSIC.length) {
        this.index = this.index + 1
        this.changeSource(this.index)
      } else {
        console.log('last song!')
        this.index = 0
        this.changeSource(this.index)
      }
    })
  }
}
</script>
<style scoped>
</style>
