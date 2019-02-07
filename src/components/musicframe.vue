<template>
  <div id="musicframe">
    <div class="title">
      <p>{{currentInfo}}</p>
    </div>
    <div class="music-info-cover">
      <img :src="currentImage" width="100%" height="100%"/>
    </div>
    <div class="buttons-wrapper player" id="controls">
      <obg-button class="prev player-buttons" icon="step-backward" @click="onClickPrev"></obg-button>
      <obg-button class="play player-buttons" :icon="isPlaying ? 'play' : 'pause'" @click="onPlay"></obg-button>
      <obg-button class="next player-buttons" icon="step-forward" @click="onClickNext"></obg-button>
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
    },
    onClickPrev () {
      bus.$emit('prev')
      console.log('prev button clicked')
    },
    onClickNext () {
      bus.$emit('next')
      console.log('next button clicked')
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
    width: 210px;
    height: 210px;
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
