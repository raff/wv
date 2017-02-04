<template>
  <div>
    <div id="waveform"></div>
    <div id="waveform-timeline"></div>
  </div>
</template>

<script>
// NOTE: added alias in webpack configuration (why would somebody name the package xxxx.js)
const WaveSurfer = require('wavesurfer')
require('wavesurfer/dist/plugin/wavesurfer.timeline')

export default {
  name: 'waveform',
  props: {
    options: {
      type: Object,
      default: function () {
        return {
          container: '#waveform',
          scrollParent: true
        }
      }
    }
  },
  data () {
    return {
      wavesurfer: null
    }
  },
  mounted () {
    this.wavesurfer = WaveSurfer.create(this.options)
    var wavesurfer = this.wavesurfer

    this.wavesurfer.on('ready', function () {
      var timeline = Object.create(WaveSurfer.Timeline)

      timeline.init({
        wavesurfer: wavesurfer,
        container: '#waveform-timeline'
      })
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- style scoped -->
<style>
.waveform {
  border: 1
}
</style>
