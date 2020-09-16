<template>
  <div id="app">
    <timeline :jsonTimeline="timelineDataJson"></timeline>
  </div>
</template>

<script>
import timeline from './components/timeline.vue'
import timelineDataJson from './assets/timeline.json'

export default {
  name: 'App',
  components: {
    timeline
  },

  data() {
    return {
      timelineDataJson: timelineDataJson
    }
  }
}
</script>
