<template>
  <div class="center-container">
    <Box>
      <CircularGauge :value="gaugeValue" />
    </Box>
  </div>
</template>

<script>
import CircularGauge from './components/CircularGauge.vue';
import Box from './components/Box.vue';

export default {
  components: {
    CircularGauge,
    Box,
  },
  data() {
    return {
      gaugeValue: 50,
    };
  },
};
</script>

<style>
.center-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
