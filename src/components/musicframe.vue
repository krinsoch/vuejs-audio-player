<template>
  <div id="musicframe">
    <div class="title">
      <p>{{currentInfo}}</p>
    </div>
    <div class="music-info-cover">
      <img :src="currentImage" width="100%" height="100%"/>
    </div>
    <div class="buttons-wrapper player" id="controls">
      <obg-button class="prev player-buttons" icon="step-backward" @click="onPrevSong"></obg-button>
      <obg-button class="play player-buttons" :icon="isPlaying ? 'play' : 'pause'" @click="onPlay"></obg-button>
      <obg-button class="next player-buttons" icon="step-forward" @click="onNextSong"></obg-button>
      <audio ref="obgAudio"
             id="audio"
             preload="auto"
             @durationchange="onUpdateDuration"
             @timeupdate="onUpdateTime"
             @progress="onProgress"
             @ended="onEnded"
             >
        <source :src="currentSong"/>
      </audio>
      <music-bar :audioInfo='audioInfo'></music-bar>
    </div>
  </div>
</template>

<script>
import {Events} from 'obigo-js-ui'
import button from 'obigo-js-ui-rnbs/components/button'
import musicBar from './music-bar'
export default {
  name: 'musicframe',
  components: {
    'obg-button': button,
    'music-bar': musicBar
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
      isPlaying: false,
      audioInfo: {
        currentTime: 0,
        duration: 0,
        buffered: 0
      }
    }
  },
  methods: {
    onPlay () {
      this.isPlaying = !this.isPlaying
    },
    onPrevSong () {
      Events.$emit('prev')
    },
    onNextSong () {
      Events.$emit('next')
    },
    onUpdateTime () {
      this.audioInfo.currentTime = this.$refs.obgAudio.currentTime
    },
    onUpdateDuration () {
      this.audioInfo.duration = this.$refs.obgAudio.duration
    },
    onProgress (e) {
      if (this.$refs.obgAudio.buffered.length === 1) {
        this.$refs.obgAudio.buffered.end(0)
      }
    },
    onEnded (e) {
      Events.$emit('next')
    }
  },
  created: function () {
    Events.$on('reload', () => {
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
  .title {
    width: 100%;
    height: 100%;
    padding: 10px 5px;
    display: inline-block;
    font-size: 1.5rem;
    text-align: center;
  }
  .music-info-cover {
    margin: 9px;
    flex: 1;
    text-align: center;
    box-sizing: border-box;
    display: block;
    width: 200px;
    height: 200px;
    margin-left: auto;
    margin-right: auto;
  }
  .buttons-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    margin: 0 auto;
  }
</style>
