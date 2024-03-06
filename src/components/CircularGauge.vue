<div class="circular-gauge">
    <canvas ref="canvas" :width="circleSize" :height="circleSize"></canvas>
    <div class="gauge-text">
      <div class="task-info">{{ name }}</div>
      <div class="task-info">Aya Count: {{ ayaCount }}</div>
      <div class="task-info">Hifd Count: {{ hifdCount }}</div>
      <div class="percentage-info">Percentage: {{ displayPercentage }}</div>
    </div>
    <div class="percentage">{{ displayPercentage }}</div>
  </div>
</template>

<script>
export default {
  props: {
    circleSize: {
      type: Number,
      default: 350
    },
    value: {
      type: Number
    },
    maxValue: {
      type: Number,
      default: 100
    },
    name: {
      type: String,
      default: 'Al Baqarah'
    },
    ayaCount: {
      type: Number,
      default: 283
    },
    hifdCount: {
      type: Number,
      default: 283
    }
  },
  computed: {
    displayPercentage() {
      const percentage = (this.value / this.maxValue) * 100
      return isNaN(percentage) ? '0%' : `${Math.round(percentage)}%`
    }
  },
  mounted() {
    this.context = this.$refs.canvas.getContext('2d')
    this.canvas = this.$refs.canvas
    this.drawGauge()
  },
  watch: {
    value() {
      this.drawGauge()
    }
  },
  methods: {
    drawGauge() {
      const { context, canvas, value } = this
      context.clearRect(0, 0, canvas.width, canvas.height)

      // Drawing the colored segment
      const coloredStartAngle = 0
      const coloredEndAngle = (value / this.maxValue) * (Math.PI * 2)

      context.beginPath()
      context.arc(
        canvas.width / 2,
        canvas.height / 2,
        canvas.width / 2 - 30,
        coloredStartAngle,
        coloredEndAngle,
        false
      )
      context.lineWidth = 40
      context.strokeStyle = '#70E094'
      context.stroke()

      // Drawing the remaining segments
      const remainingStartAngle = coloredEndAngle
      const remainingEndAngle = Math.PI * 2

      const numSegments = 10
      const spaceAtBothSides = 0.05
      const spaceBetweenSegments = 0.1
      const totalSpace = spaceAtBothSides * 2 + spaceBetweenSegments * (numSegments - 1)
      const availableSpace = remainingEndAngle - remainingStartAngle - totalSpace
      const segmentAngle = availableSpace / numSegments

      for (let i = 0; i < numSegments; i++) {
        context.beginPath()
        const startAngle =
          remainingStartAngle + spaceAtBothSides + (segmentAngle + spaceBetweenSegments) * i
        const endAngle = startAngle + segmentAngle

        // Adjust the radius value to control the border radius
        const radius = canvas.width / 2 - 30
        const x = canvas.width / 2
        const y = canvas.height / 2

        // Draw the arc with border radius
        context.arc(x, y, radius, startAngle, endAngle, false)
        context.lineWidth = 40
        context.strokeStyle = '#333333'
        context.stroke()
      }
    }
  }
}
</script>

<style scoped>
.circular-gauge {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}

.gauge-text {
  position: absolute;
  top: 45%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  margin: auto;
}

.task-info,
.percentage-info {
  font-size: 20px;
  color: #ffffff;
}

.percentage {
  display: inline-block;
  padding: 3px 15px;
  color: black;
  font-style: italic;
  background-color: white;
  border-radius: 20px;
  transform: translateX(9rem) translateY(-11rem);
  z-index: 2;
}

.circular-gauge canvas {
  z-index: 1;
}

.task-info,
.percentage-info {
  font-size: 20px;
  color: #ffffff;
}

.circular-gauge canvas.colored-segment {
  z-index: 1;
  background-color: #70e094;
}

.circular-gauge canvas.remaining-segment {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  background-color: #f0f0f0;
}
</style>