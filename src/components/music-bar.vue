<template>
  <div class="progressbar-wrapper">
    <obg-progress :value=value :width=300 >
      <span slot='start'>{{currentTime}}</span>
      <span slot='end'>{{duration}}</span>
    </obg-progress>
  </div>
</template>

<script>
import progressBar from 'obigo-js-ui/components/progress'
export default{
  name: 'music-bar',
  components: {
    'obg-progress': progressBar
  },
  props: ['audioInfo'],
  computed: {
    currentTime: function () {
      return this.secToTime(this.audioInfo.currentTime)
    },
    duration: function () {
      return this.secToTime(this.audioInfo.duration)
    },
    value: function () {
      const length = Math.round(this.audioInfo.currentTime / this.audioInfo.duration * 100)
      return isNaN(length) ? 0 : length
    }
  },
  methods: {
    secToTime: (sec) => {
      let date = new Date(null)
      let timeStr = 1
      const regex = /^(00)+:[0-5]?\d:[0-5]?\d/
      date.setSeconds(Math.round(sec))
      timeStr = date.toISOString().substr(11, 8)
      if (regex.exec(timeStr)) {
        return timeStr.substr(3, 6)
      } else {
        return timeStr
      }
    }
  }
}
</script>

<style scoped>
  .progressbar-wrapper{
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 15px;
    position: absolute;
    bottom: 80px;
}
.progressBar{
    margin: 0px auto;
    position: inherit;
    background: rgb(0, 0, 0);
    width: 280px;
    margin: 5px;
}
.buffer{
}
</style>
