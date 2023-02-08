<template>
  <div class="chart-wrap">
    <div class="chart-online">
      <div class="chart-container">
        <highcharts class="online-pie" :options="chartOptions"></highcharts>
      </div>
      <span class="chart-count"></span>
    </div>
    <div class="chart-offline">
      <div class="chart-container"></div>
      <span class="chart-count"></span>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, watch } from "vue";
import { Chart } from "highcharts-vue";
export default defineComponent({
  name: "countryChart",
  props: {
    chartData: Object,
    default: () => {
      return;
    },
  },
  components: {
    highcharts: Chart,
  },
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  setup(props, { emit }) {
    return {
      chartOptions: {
        chart: {
          type: "pie",
        },
        title: {
          text: "",
        },
        colors: ["#00adef", "#ffde68", "#f06280", "#ff8c38"],
        tooltip: {
          pointFormat: "{series.name}: <b>{point.percentage:.1f}%</b>",
        },
        accessibility: {
          enabled: false,
        },
        plotOptions: {
          pie: {
            // size: "100%",
            allowPointSelect: true,
            cursor: "pointer",
          },
        },
        series: [{}],
        legend: {
          layout: "horizontal",
          align: "center",
          verticalAlign: "top",
          x: -3,
          y: -2,
        },
      },
    };
  },
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  created() {},
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  mounted() {},
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  unmounted() {},
  methods: {},
});
</script>
<style scoped lang="scss">
.chart-wrap {
  width: 100%;
  height: 250px;
  margin: 34px auto 0;
  display: flex;

  .chart-online {
    flex: 1;
  }

  .chart-offline {
    margin-left: 165px;
  }

  .chart-container {
    width: 100%;
    height: 240px;
  }

  .chart-count {
    display: block;
    height: 14px;
    margin-top: 16px;
    font-family: "actual", "Noto Sans KR";
    font-size: 12px;
    line-height: 29px;
    color: #333;
  }

  .online-pie {
    height: 280px;
  }
}
</style>
