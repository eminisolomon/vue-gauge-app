<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
</script>

<template>
  <div class="gauge-box">
    <div class="gauge-content">
      <div class="gauge-icon">
        <font-awesome-icon icon="chart-line" class="icon" />
      </div>
      <div class="gauge-text">Surah</div>
    </div>
    <div class="gauge-container">
      <slot></slot>
    </div>
  </div>
</template>

<style scoped>
.gauge-box {
  position: relative;
  width: 500px;
  max-width: 700px;
  height: calc(100vw + 20px);
  background-color: #202020;
  border-radius: 25px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 10px;
  margin: 0 5px;
}


.gauge-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.gauge-content {
  display: flex;
  align-items: center;
}

.gauge-icon {
  margin-right: 10px;
}

.icon {
  font-size: 24px;
  color: #4caf50;
}

.gauge-text {
  color: #fff;
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 5px;
}

@media (min-width: 768px) {
  .gauge-box {
    height: 500px;
  }

  .gauge-text {
    font-size: 24px;
    margin-bottom: 20px;
  }
}
</style>
