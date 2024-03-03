<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
</script>

<template>
  <div class="gauge-box">
    <div class="gauge-icon">
      <font-awesome-icon icon="chart-line" class="icon" />
    </div>
    <div class="gauge-text">Revenue</div>
    <slot></slot>
  </div>
</template>

<style scoped>
.gauge-box {
  position: relative;
  width: calc(100vw - 10px);
  margin: 0 5px;
  max-width: 700px;
  height: 90vw;
  background-color: #202020;
  border-radius: 25px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.gauge-icon {
  position: absolute;
  top: 10px;
  left: 10px;
}

.icon {
  font-size: 24px;
  color: #4caf50;
  margin-right: 10px;
}

.gauge-text {
  position: absolute;
  top: 10px;
  left: 40px;
  color: #fff;
  font-size: 18px;
  font-weight: bold;
}

@media (min-width: 768px) {
  .gauge-box {
    width: 500px;
    height: 500px;
  }

  .gauge-text {
    font-size: 24px;
    left: 60px;
  }
}
</style>
