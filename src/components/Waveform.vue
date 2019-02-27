<template>
  <div>
    <div id="waveform"></div>
    <div id="waveform-timeline"></div>
  </div>
</template>

<script>
import WaveSurfer from 'wavesurfer.js';
import TimelinePlugin from 'wavesurfer.js/dist/plugin/wavesurfer.timeline.min.js';
import RegionsPlugin from 'wavesurfer.js/dist/plugin/wavesurfer.regions.min.js';

export default {
  name: 'waveform',
  props: {
    options: {
      type: Object,
      default: function () {
        return {
          container: '#waveform',
          scrollParent: true,
          plugins: [
            TimelinePlugin.create({container: '#waveform-timeline'}),
            RegionsPlugin.create()
          ]
        }
      }
    }
  },
  data () {
    return {
      wavesurfer: null,
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
