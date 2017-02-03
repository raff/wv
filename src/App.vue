<template>
  <div id="app">
    <input type="file" name="file" class="btn btn-primary" @change="onFileChange">
    <waveform ref="wf"></waveform>
    <button type="button" class="btn btn-primary" @click="onPlayPause">
      <span v-if="playing">
        <icon name="fa-pause"></icon> Pause
      </span>
      <span v-else>
        <icon name="fa-play"></icon> Play
      </span>
    </button>
  </div>
</template>

<script>
import Waveform from './components/Waveform'
import Icon from 'vue-icons'

export default {
  name: 'app',
  components: {
    Waveform,
    Icon
  },
  data () {
    return {
      playing: false
    }
  },
  methods: {
    onFileChange: function (e) {
      if (e.target.files.length > 0) {
        this.$refs.wf.wavesurfer.loadBlob(e.target.files[0])
      }
    },
    onPlayPause: function (e) {
      this.$refs.wf.wavesurfer.playPause()
      this.playing = this.$refs.wf.wavesurfer.isPlaying()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
