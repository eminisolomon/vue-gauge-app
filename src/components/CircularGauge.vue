<template>
    <div class="circular-gauge">
      <canvas ref="canvas" :width="circleSize" :height="circleSize"></canvas>
      <div class="gauge-text">
        <div class="task-info">Total Task: {{ totalTasks }}</div>
        <div class="task-info">Done Tasks: {{ doneTasks }}</div>
        <div class="percentage-info">Percentage: {{ displayPercentage }}</div>
      </div>
      <div className="percentage">65%</div>
    </div>
  </template>
  
  <script>
import { withCtx } from 'vue';

  export default {
    data() {
      return {
        circleSize: 350,
        context: null,
        value: 65,
        maxValue: 100,
        linesCount: 10,
        totalTasks: 87,
        doneTasks: 34,
      };
    },
    computed: {
      percentage() {
        return (this.value / this.maxValue) * 100;
      },
      displayPercentage() {
        return isNaN(this.percentage) ? '0%' : `${Math.round(this.percentage)}%`;
      },
    },
    mounted() {
      this.context = this.$refs.canvas.getContext('2d');
      this.canvas = this.$refs.canvas;
      this.drawGauge();
    },
    watch: {
      value() {
        this.drawGauge();
      },
    },
    methods: {
      drawGauge() {
        const { context, circleSize, value, maxValue, linesCount, canvas } = this;
        // context.clearRect(0, 0, circleSize, circleSize);
  
        // const lineWidth = 50;
        // const gaugeCircleRadius = (circleSize - lineWidth) / 2;
        // const progressCircleRadius = (circleSize - lineWidth) / 2;
  
        // context.beginPath();
        // context.arc(circleSize / 2, circleSize / 2, gaugeCircleRadius, 0, 2 * Math.PI);
        // context.strokeStyle = '#ccc';
        // context.lineWidth = lineWidth;
        // context.stroke();
  
        // const percentage = (value / maxValue) * 100;
        // const angle = (percentage / 100) * 2 * Math.PI;
  
        // context.beginPath();
        // context.arc(circleSize / 2, circleSize / 2, progressCircleRadius, -Math.PI / 2, -Math.PI / 2 + angle);
        // context.strokeStyle = '#4caf50';
        // context.lineWidth = lineWidth;
        // context.stroke();
  
        // // Display the percentage at the end of the green line
        // const textX = circleSize / 2 + progressCircleRadius * Math.cos(-Math.PI / 2 + angle);
        // const textY = circleSize / 2 + progressCircleRadius * Math.sin(-Math.PI / 2 + angle);
  
        // const textPadding = 5;
        // const textWidth = context.measureText(`${Math.round(percentage)}%`).width;
        // const textHeight = 20;
  
        // context.fillStyle = '#4caf50';
        // context.font = '20px Arial';
        // context.textAlign = 'center';
        // context.textBaseline = 'middle';
  
        // const adjustedTextX = Math.min(circleSize - textWidth - textPadding, Math.max(textWidth + textPadding, textX));
        // const adjustedTextY = Math.min(circleSize - textHeight - textPadding, Math.max(textHeight + textPadding, textY));
  
        // context.fillText(`${Math.round(percentage)}%`, adjustedTextX, adjustedTextY);
  
        // // Draw the remaining lines
        // const remainingLinesAngle = angle;
        // const remainingLinesGap = (2 * Math.PI - remainingLinesAngle) / (linesCount - 1);
  
        // for (let i = 0; i < linesCount; i++) {
        //   const startAngle = -Math.PI / 2 + remainingLinesAngle + i * remainingLinesGap;
        //   const endAngle = -Math.PI / 2 + remainingLinesAngle + i * remainingLinesGap + remainingLinesGap;
  
        //   context.beginPath();
        //   context.arc(circleSize / 2, circleSize / 2, progressCircleRadius, startAngle, endAngle);
        //   context.strokeStyle = '#fff';
        //   context.lineWidth = lineWidth;
        //   context.stroke();
        // }


        // Define the number of segments and gap size
        const numSegments = 25;
        const gapSize = 0.2;

        // Calculate the angle per segment and gap
        const segmentAngle = (Math.PI * 2) / (numSegments + gapSize * (numSegments - 1));
        const gapAngle = gapSize * segmentAngle;

        // Calculae the size for the main angle
        const coloredSegmentSize = Math.round(0.65 * 25);
        const coloredStartAngle = 0;
        const coloredEndAngle = (coloredSegmentSize * (segmentAngle + gapAngle)) + segmentAngle - 0.03;
        
        context.beginPath();
        context.arc(canvas.width / 2, canvas.height / 2, canvas.width / 2 - 15, coloredStartAngle, coloredEndAngle, false);
        context.lineWidth = 30;
        context.strokeStyle = '#70E094';
        context.stroke();

        for(let i = 0; i < (numSegments - coloredSegmentSize) - 1; i++){
          // Calculate the starting and ending angle for each segment
          const startAngle = (i * (segmentAngle + gapAngle)) + coloredEndAngle + segmentAngle - 0.155;
          const endAngle = startAngle + segmentAngle - 0.03;

          // Draw the arc for each segment
          context.beginPath();
          context.arc(canvas.width / 2, canvas.height / 2, canvas.width / 2 - 15, startAngle, endAngle, false);

          // if(startAngle < percentage){
          //   context.strokeStyle = '#4caf50';
          // } else {
            context.strokeStyle = '#fff';
          // }

          context.lineWidth = 30;
          context.stroke();
        }

      },
    },
  };
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
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
  }
  
  .task-info, .percentage-info {
    font-size: 20px;
    color: #FFFFFF;
  }

  .percentage {
    display: inline-block;
    padding: 3px 15px;
    color: black;
    font-style: italic;
    background-color: white;
    border-radius: 20px;
    transform: translateX(10rem) translateY(-10rem);
  }
  </style>
  