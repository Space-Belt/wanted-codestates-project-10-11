<template>
  <RadarChart :chartData="matchData" />
</template>

<script>
import { defineComponent } from 'vue';
import { RadarChart } from 'vue-chart-3';
import { Chart, registerables } from 'chart.js';
import referenceData from '../ReferenceData';

Chart.register(...registerables);
export default defineComponent({
  name: 'Home',
  components: { RadarChart },
  setup() {
    const testData = {
      labels: [
        ['적극적인', 'Aggressive', ''],
        ['  자신있는', 'Confident', ''],
        ['', '    책임있는', 'Responsible'],
        ['', '개인주의  ', 'Indivisual'],
        ['수평적인   ', 'Horizontal', ''],
      ],
      datasets: [
        {
          data: referenceData['삼성'],
          backgroundColor: 'rgba(255, 193, 74, 0.32)',
          borderColor: ' #FFD335',
          pointRadius: 0,
          borderWidth: 2,
        },
        {
          data: referenceData['user'],
          backgroundColor: 'rgba(110, 60, 249, 0.32)',
          borderColor: ' #6E3CF9',
          pointRadius: 0,
          borderWidth: 2,
        },
        {
          data: [10, 10, 10, 10, 10],
          backgroundColor: 'rgba(248, 248, 248, 0.32)',
          borderColor: ' #B2B2B2',
          pointRadius: 13,
          borderWidth: 1,
          pointBackgroundColor: [
            'rgba(235, 133, 108, 0.7)',
            'rgba(108, 135, 245, 0.5)',
            'rgba(64, 171, 199, 0.5)',
            'rgba(229, 115, 160, 0.5)',
            'rgba(101, 184, 81, 0.5)',
          ],
          pointBorderColor: [
            'rgba(235, 133, 108, 0.7)',
            'rgba(108, 135, 245, 0.5)',
            'rgba(64, 171, 199, 0.5)',
            'rgba(229, 115, 160, 0.5)',
            'rgba(101, 184, 81, 0.5)',
          ],
          pointBorderWidth: 1,
          pointHoverRadius: 1,
        },
      ],
    };

    return { testData };
  },
  props: {
    searchData: String,
  },
  data() {
    return {
      matchData: this.testData,
    };
  },
  beforeMount() {
    Chart.defaults.hover = { mode: null };
    const { plugins, scale } = Chart.defaults;
    plugins.legend.display = false;
    plugins.tooltip.enabled = false;
    Chart.defaults.font = {
      family: "'Helvetica Neue', 'Helvetica', 'Arial', sans-serif",
      lineHeight: 1.2,
      size: 15,
      style: 'normal',
      weight: 'bold',
    };
    scale.ticks = {
      max: 10,
      min: 0,
      stepSize: 2,
      display: false,
    };
    scale.grid.borderDash = [4];
  },
  mounted() {
    switch (this.searchData) {
      case '삼성':
        this.matchData.datasets[0].data = [...referenceData['삼성']];
        break;
      case '카카오':
        this.matchData.datasets[0].data = [...referenceData['카카오']];
        break;
      case 'lg':
        this.matchData.datasets[0].data = [...referenceData['lg']];
        break;
      default:
        this.matchData.datasets[0].data = [0, 0, 0, 0, 0];
        break;
    }
  },
});
</script>
