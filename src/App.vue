<template>
  <div id="app">
    <input type="file" name="file" class="btn btn-primary" @change="onFileChange">
    <waveform ref="wf"></waveform>
    <button type="button" class="btn btn-primary" @click="onPlayPause">
      <span v-if="playing">
        <fa :icon="faPause"/> Pause
      </span>
      <span v-else>
        <fa :icon="faPlay"/> Play
      </span>
    </button>

    <span>&nbsp;&nbsp;&nbsp;</span>

    <button type="button" class="btn btn-primary" @click="onPlayNote">
      <span v-if="looping">
        <fa :icon="faPause"/> Clear
      </span>
      <span v-else>
        <fa :icon="faPlay"/> Loop
      </span>
    </button>

    <span>&nbsp;&nbsp;&nbsp;</span>

    <input type="radio" name="speed" v-model="speed" value="0.25"> 25&#37;
    <input type="radio" name="speed" v-model="speed" value="0.50"> 50&#37;
    <input type="radio" name="speed" v-model="speed" value="0.75"> 75&#37;
    <input type="radio" name="speed" v-model="speed" value="0.80"> 80&#37;
    <input type="radio" name="speed" v-model="speed" value="0.90"> 90&#37;
    <input type="radio" name="speed" v-model="speed" value="1.00">100&#37;
    <input type="radio" name="speed" v-model="speed" value="1.50">150&#37;

  </div>
</template>

<script>
import Waveform from './components/Waveform'
import Fa from 'vue-fa'
import { faPlay, faPause } from '@fortawesome/free-solid-svg-icons'


export default {
  name: 'app',
  components: {
    Waveform,
    Fa
  },
  data () {
    return {
      playing: false,
      looping: false,
      speed: "1.00",
      faPlay,
      faPause
    }
  },
  watch: {
    // eslint-disable-next-line
    speed: function(val, old) {
        this.$refs.wf.wavesurfer.setPlaybackRate(val)
    }
  },
  methods: {
    onFileChange: function (e) {
      if (e.target.files.length > 0) {
        var ws = this.$refs.wf.wavesurfer
        ws.clearRegions()
        ws.loadBlob(e.target.files[0])
      }
    },

    // eslint-disable-next-line
    onPlayPause: function (e) {
      var ws = this.$refs.wf.wavesurfer
      if (ws.isPlaying()) {
        this.playing = false
        ws.pause()
      } else {
        this.playing = true
        ws.play()
      }
    },

    // eslint-disable-next-line
    onPlayNote: function (e) {
      var ws = this.$refs.wf.wavesurfer
      ws.clearRegions()

      //this.playing = ws.isPlaying()

      if (!this.looping) {
          var curr = ws.getCurrentTime()

          var r = ws.addRegion({
            id: "loop",
            start: curr,
            end: curr + 0.1,
            color: 'rgba(0.0, 1.0, 0.0, 0.0)',
            loop: true
          })

          r.play()
          ws.play()
          this.looping = true;
      } else {
          this.looping = false;
          if (!this.playing) {
            ws.pause()
          }
      }
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
