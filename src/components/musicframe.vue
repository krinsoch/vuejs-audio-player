<template>
  <div id="musicframe">
    <div class="title">
      <p>{{currentInfo}}</p>
    </div>
    <div class="img">
      <img :src="currentImage" width="100%" height="100%"/>
    </div>
    <div class="btm" id="controls">
      <obg-button :icon="isPlaying ? 'play' : 'pause'" @click="onPlay"></obg-button>
      <audio controls ref="obgAudio"
             id="audio"
             preload="auto"
             loop="true"
             >
        <source :src="currentSong"/>
      </audio>
    </div>
  </div>
</template>

<script>
import {bus} from '../main'
import button from 'obigo-js-ui-rnbs/components/button'
export default {
  name: 'musicframe',
  components: {
    'obg-button': button
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
      isPlaying: false
    }
  },
  methods: {
    onPlay () {
      this.isPlaying = !this.isPlaying
    },
    muted () {
      return this.$refs.obgAudio.muted
    },
    mute () {
      let isMuted = this.muted()
      this.$refs.obgAudio.muted = !this.$refs.obgAudio.muted
      if (!isMuted) {
        console.log('playing->mute')
      } else {
        console.log('mute->play')
      }
    }
  },
  created: function () {
    bus.$on('reload', () => {
      this.$refs.obgAudio.load()
      this.$refs.obgAudio.play()
    })
  },
  updated () {
    if (!this.isPlaying) {
      this.$refs.obgAudio.play()
      console.log('play music')
    } else {
      this.$refs.obgAudio.pause()
      console.log('stop music')
    }
  }
}
</script>
<style lang='scss' scoped>
.contents {
  padding:20px;
  color: white;
  & > p,
  & > div{
    padding:20px;
  }
}
  img {
    border: 1px;
    border-radius: 4px;
    padding: 10px;
  }
  .title {
    width: 100%;
    height: 100%;
    padding: 10px 5px;
    display: inline-block;
    font-size: 1.5rem;
    text-align: center;
  }
  #controls {
    border: none;
    color: white;
    position: absolute;
    top: 280px;
    width: 400px;
    height: 80px;
    text-align: center;
  }
  .audio {
    float: right;
  }
</style>
