<template>
  <div id="musicframe">
    <marquee>{{currentInfo}}</marquee>
    <div class="img">
      <img v-bind:src="currentImage" width="100%" height="100%"/>
    </div>
    <div class="btm" id="controls">
      <audio ref="audio" id="audio">
        <source v-bind:src="currentSong"/>
        not supported
      </audio>
      <span class="btn fa fa-play fa-4x" v-on:click="play"></span>
      <span class="btn fa fa-pause fa-4x" v-on:click="pause"></span>
    </div>
  </div>
</template>

<script>
import {bus} from '../main'
export default {
  name: 'musicframe',
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
    }
  },
  methods: {
    play () {
      console.log('Clicked Play Button')
      this.$refs.audio.play()
    },
    pause () {
      console.log('Clicked Pause Button')
      this.$refs.audio.pause()
    }
  },
  created: function () {
    bus.$on('reload', () => {
      this.$refs.audio.load()
      this.$refs.audio.play()
    })
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
  .img {
    height: auto;
  }
  img {
    border: 1px;
    border-radius: 4px;
    padding: 10px;
  }
  marquee {
    width: 100%;
    height: 40px;
    margin: 5px;
    display: block;
    font-size: 30px;
    text-align: center;
  }
  #controls {
    border: none;
    color: white;
    font-size: 1em;
    position: absolute;
    top: 280px;
    width: 400px;
    height: 100px;
    text-align: center;
  }
  .btn {
    width: 5rem;
  }
</style>
