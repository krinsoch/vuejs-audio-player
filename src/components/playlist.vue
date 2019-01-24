<template>
  <div id="playlist">
    <div id="secborder" ref="playlist" @click="changeSource">
      <div class="song" url-value="http://img0.liveinternet.ru/images/attach/b/3/3656/3656927_eminem__mockingbird.mp3" picture-value="https://wallpapercave.com/wp/WlHnNj6.jpg" info-value="Eminem - Mocking Bird">Eminem - Mocking Bird</div>
      <div class="song" url-value="http://soundbible.com/mp3/Air%20Plane%20Ding-SoundBible.com-496729130.mp3" picture-value="https://orig00.deviantart.net/65e3/f/2009/335/6/2/linkin_park__faint_by_jimeye.jpg" info-value="Linkin Park - Faint">Linkin Park - Faint</div>
      <div class="song" url-value="http://rm.sina.com.cn/wm/VZ2008072314565310537VK/music/MUSIC0807231507294087.mp3" picture-value="https://i.ytimg.com/vi/oY5BYjsrIHk/maxresdefault.jpg" info-value="Linkin Park - Somewhere I belong">Linkin Park - Somewhere I belong</div>
      <div class="song" url-value="http://a.tumblr.com/tumblr_mirhiitqaC1roewk4o1_r1.mp3" picture-value="https://i.ytimg.com/vi/vAsztnDeZ1Q/maxresdefault.jpg" info-value="Demi Lovato - Heart Attack">Demi Lovato - Heart Attack</div> 
      <div class="song" url-value="@/Kalimba.mp3" picture-value="https://orig00.deviantart.net/65e3/f/2009/335/6/2/linkin_park__faint_by_jimeye.jpg"> local - kalimba </div>
      <div class="song" url-value="@/src/asset/Kalimba.mp3" picture-value="https://orig00.deviantart.net/65e3/f/2009/335/6/2/linkin_park__faint_by_jimeye.jpg"> local - kalimba </div>
      <div class="song" url-value="C:\Users\krinsoch\Documents\workspace\MyApp\src\asset\Kalimba.mp3" picture-value="https://orig00.deviantart.net/65e3/f/2009/335/6/2/linkin_park__faint_by_jimeye.jpg"> local - kalimba </div>
      <div class="song" url-value="C:\Users\krinsoch\Documents\workspace\MyApp\src\asset\Kalimba.mp3" picture-value="https://orig00.deviantart.net/65e3/f/2009/335/6/2/linkin_park__faint_by_jimeye.jpg"> local - kalimba </div>
      <div class="song" url-value="C:\Users\krinsoch\Documents\workspace\MyApp\src\asset\Kalimba.mp3" picture-value="https://orig00.deviantart.net/65e3/f/2009/335/6/2/linkin_park__faint_by_jimeye.jpg"> local - kalimba </div>
      <div class="song" url-value="C:\Users\krinsoch\Documents\workspace\MyApp\src\asset\Kalimba.mp3" picture-value="https://orig00.deviantart.net/65e3/f/2009/335/6/2/linkin_park__faint_by_jimeye.jpg"> local - kalimba </div>
      <div class="song" url-value="C:\Users\krinsoch\Documents\workspace\MyApp\src\asset\Kalimba.mp3" picture-value="https://orig00.deviantart.net/65e3/f/2009/335/6/2/linkin_park__faint_by_jimeye.jpg"> local - kalimba </div>
    </div>
  </div>
</template>

<script>
import { bus } from '../main'
export default {
  name: 'playlist',
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
    changeSource: function (e) {
      let songValue = e.target.attributes[1].nodeValue
      let songImage = e.target.attributes[2].nodeValue
      let songInfo = e.target.attributes[3].value
      console.log(songValue, songImage, songInfo, 'playlist changSource log')
      this.$emit('updateData', [songValue, songImage, songInfo])
      bus.$emit('reload')
    }
  }
}
</script>
<style scoped>
#secborder {
    border: 5px solid white;
    border-radius: 15px;
    margin: 2rem 0.5rem;
    background: black;
    height: 300px; /* 20srem; */
    width: 380px;
    overflow: scroll;
}
.song {
    width: 100%;
    height: auto;
    padding: 0.5em;
    border-bottom: 0.5px solid #172951;
    font-size: 1.5rem;
    font-weight: bold;
    text-align: center;
    color: white;
    cursor: pointer;
}
</style>
