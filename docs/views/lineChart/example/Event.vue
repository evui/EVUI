<template>
  <div class="case">
    <ev-chart
      :data="chartData"
      :options="chartOptions"
      @click="onClick"
      @dbl-click="onDblClick"
    />
    <div class="description">
      <div class="badge yellow">
        클릭된 라벨
      </div>
      {{ clickedLabel }}
      <br><br>
      <div class="badge yellow">
        더블 클릭된 라벨
      </div>
      {{ dblClickedLabel }}
    </div>
  </div>
</template>

<script>
  import { ref } from 'vue';
  import moment from 'moment';

  export default {
    setup() {
      const time = moment().format('YYYY-MM-DD');
      const chartData = {
        series: {
          series1: { name: 'series#1' },
          series2: { name: 'series#2' },
        },
        labels: [
          moment(time),
          moment(time).add(1, 'day'),
          moment(time).add(2, 'day'),
          moment(time).add(3, 'day'),
          moment(time).add(4, 'day'),
          moment(time).add(5, 'day'),
          moment(time).add(6, 'day'),
        ],
        data: {
          series1: [100, 25, 36, 47, 0, 50, 80],
          series2: [80, 36, 25, 47, 15, 100, 0],
        },
      };

      const chartOptions = {
        type: 'line',
        width: '100%',
        title: {
          text: 'Chart Title',
          show: true,
        },
        legend: {
          show: true,
          position: 'right',
        },
        axesX: [{
          type: 'time',
          showGrid: false,
          categoryMode: true,
          timeFormat: 'YYYY-MM-DD',
          interval: 'day',
        }],
        axesY: [{
          type: 'linear',
          showGrid: true,
          startToZero: true,
          autoScaleRatio: 0.1,
        }],
        selectItem: {
          use: true,
          showTextTip: true,
        },
      };

      const clickedLabel = ref("''");
      const onClick = (target) => {
        clickedLabel.value = target.label;
      };

      const dblClickedLabel = ref("''");
      const onDblClick = (target) => {
        dblClickedLabel.value = target.label;
      };

      return {
        chartData,
        chartOptions,
        clickedLabel,
        dblClickedLabel,
        onClick,
        onDblClick,
      };
    },
  };
</script>

<style lang="scss">
</style>
