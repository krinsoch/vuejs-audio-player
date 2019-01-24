<template>
  <div class='row'>
    <div class='column'>
      <musicframe v-bind:currentSong="currentSong" v-bind:currentImage="currentImage" v-bind:currentInfo="currentInfo"></musicframe>
    </div>
    <div class='column'>
      <playlist v-bind:currentSong="currentSong" v-bind:currentImage="currentImage" v-bind:currentInfo="currentInfo" @updateData="swapData($event)"></playlist>
    </div>
  </div>
</template>

<script>
import page from 'obigo-js-ui/mixins/page'
import playlist from './playlist'
import musicframe from './musicframe'
export default {
  name: 'home',
  mixins: [page],
  components: {
    'playlist': playlist,
    'musicframe': musicframe
  },
  data () {
    return {
      currentSong: '',
      currentImage: 'https://i.ibb.co/Xxc5QT7/001.jpg',
      currentInfo: 'Audio Player'
    }
  },
  methods: {
    swapData: function (data) {
      this.currentSong = data[0]
      this.currentImage = data[1]
      this.currentInfo = data[2]
    }
  }
}
</script>
<style lang='scss' scoped>
/*.contents {
  padding:20px;
  color: white;
  & > p,
  & > div{
    padding:20px;
  }
}*/
  .row {
    display: flex;
    height: 100%;
  }
  .column {
    flex: 50%;
    height: 100%;
  }

@mixin mx-carmodel-7pr {
  .contents {
    color: gray;
  }
}

@mixin mx-carmodel-7pd {
  .contents {
    color: cyan;
  }
}

@mixin mx-carmodel-9pr {
  .contents {
    color: yellow;
  }
}

@mixin get-style-of($model) {
  @if $model == '7pr' {
    @include mx-carmodel-7pr;
  }

  @if $model == '9pr' {
    @include mx-carmodel-9pr;
  }

  @if $model == '7pd' {
    @include mx-carmodel-7pd;
  }
}

@if $profile == 'production' {
  @media renault7P {
    @include get-style-of('7pr');
  }

  @media renault9P {
    @include get-style-of('9pr');
  }

  @media dacia7P {
    @include get-style-of('7pd');
  }
} @else {
  @include get-style-of($car-model)
}
</style>
