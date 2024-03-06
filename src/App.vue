<template>
  <div class="center-container">
    <Box :title="boxTitle">
      <CircularGauge
        :value="gaugeValue"
        :circleSize="gaugeSize"
        :name="gaugeName"
        :ayaCount="gaugeAyaCount"
        :hifdCount="gaugeHifdCount"
      />
    </Box>
  </div>
</template>

<script>
import CircularGauge from './components/CircularGauge.vue'
import Box from './components/Box.vue'

export default {
  components: {
    CircularGauge,
    Box
  },
  data() {
    return {
      gaugeValue: 65,
      gaugeSize: 400,
      gaugeName: 'Al Baqarah',
      gaugeAyaCount: 283,
      gaugeHifdCount: 283,
      boxTitle: 'Gauge Box'
    }
  }
}
</script>

<style>
.center-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
