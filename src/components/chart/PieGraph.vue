<template>
  <div class="chart-wrap">
    <div class="chart-online">
      <div class="chart-container">
        <highcharts class="online-pie" :options="chartOptions"></highcharts>
      </div>
      <span class="chart-count"></span>
    </div>
    <div class="chart-offline">
      <div class="chart-container">
        <!-- <highcharts class="offline-pie" :options="chartOptions"></highcharts> -->
      </div>
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
    normalOn: Number,
    warningOn: Number,
    errorOn: Number,
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
            dataLabels: {
              enabled: true,
            },
            allowPointSelect: true,
            cursor: "pointer",
            showInLegend: true,
          },
        },
        series: [
          {
            type: "pie",
            name: "",
            colorByPoint: true,
            innerSize: "0%",
            data: [
              {
                name: "Chrome",
                y: 74.77,
                sliced: true,
                selected: true,
              },
              {
                name: "Edge",
                y: 12.82,
              },
              {
                name: "Firefox",
                y: 4.63,
              },
              {
                name: "Safari",
                y: 2.44,
              },
              {
                name: "Internet Explorer",
                y: 2.02,
              },
              {
                name: "Other",
                y: 3.28,
              },
            ],
          },
        ],
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
  height: 250px;
  margin: 34px auto 0;
  display: flex;
  box-sizing: border-box;
  // box-sizing: border-box;

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

  .offline-pie {
    height: 280px;
  }
}
</style>
