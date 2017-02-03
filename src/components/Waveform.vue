<template>
  <div id="waveform">
  </div>
</template>

<script>
import WaveSurfer from 'wavesurfer.js'

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
