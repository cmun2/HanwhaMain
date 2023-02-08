<template>
  <div class="chart-summary">
    <div class="country-opt">
      <div class="option">
        <div class="country-all-filter">
          <div class="checkbox-all">
            <input
              type="checkbox"
              value="All"
              v-model="allChecked"
              @click="allClick"
            />
            <label for="All">All</label>
          </div>
        </div>
        <div class="country-filter">
          <div
            class="checkbox-country"
            :key="index"
            v-for="(chart, index) in chartData"
          >
            <input
              type="checkbox"
              :key="index"
              v-model="checkedCountry"
              :value="chart.countryCd"
              @change="countryClick"
            />
            <label for="Country" :key="index + '1'">{{
              chart.countryCd
            }}</label>
          </div>
        </div>
        <span>check: {{ checkedCountry }}</span>
        <span>check: {{ allChecked }}</span>
      </div>
      <div class="option-result">
        <div class="count-total">
          <span
            >Product
            <strong>0</strong>
          </span>
          <span
            >Installed Last Week
            <strong>0</strong>
          </span>
        </div>
        <PieGraph :chartData="chartData" />
      </div>
    </div>
    <!-- <PieGraph /> -->
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, watch, ref, Ref, computed } from "vue";
import PieGraph from "./PieGraph.vue";
// import * as HighCharts from "highcharts";

// const defaultChartOption: HighCharts.Options = Object.freeze({
//   chart: {
//     type: "pie",
//     height: "240px",
//   },
//   accessibility: {
//     point: {
//       valueSuffix: "%",
//     },
//   },
// });

export default defineComponent({
  components: {
    PieGraph,
  },
  props: {
    chartData: {
      type: Object,
      default: () => {
        return;
      },
    },
  },
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  setup(props, { emit }) {
    const countryList = props.chartData.map((list: any) => {
      return list.countryCd;
    });

    let checkedCountry: Ref<string[]> = ref([]);

    for (let i = 0; i < countryList.length; i++) {
      checkedCountry.value.push(String(countryList[i]));
    }

    let allChecked = ref(true);

    // const allClick = () => {
    //   if (!allChecked.value && checkedCountry.value.length != 0) {
    //     checkedCountry.value = [];
    //     for (let i = 0; i < countryList.length; i++) {
    //       checkedCountry.value.push(String(countryList[i]));
    //     }
    //     allChecked.value = true;
    //   } else {
    //     checkedCountry.value = [];
    //     allChecked.value = false;
    //   }
    // };

    const allClick = () => {
      if (!allChecked.value) {
        if (checkedCountry.value.length != 0) {
          checkedCountry.value = [];
        }
        for (let i = 0; i < countryList.length; i++) {
          checkedCountry.value.push(String(countryList[i]));
        }
        allChecked.value = true;
      } else {
        checkedCountry.value = [];
        allChecked.value = false;
      }
    };

    const countryClick = () => {
      console.log(checkedCountry.value);
      if (checkedCountry.value.length === countryList.length) {
        allChecked.value = true;
      } else {
        allChecked.value = false;
      }
    };

    const selectedCountry = reactive(
      computed(() => {
        return emit("checkedCountry", checkedCountry.value);
      })
    );

    console.log(checkedCountry);

    return {
      allClick,
      allChecked,
      checkedCountry,
      selectedCountry,
      countryClick,
    };

    // let checkedAll = ref(true);
    // const checkAll = () => {
    //   !(checkedAll.value) {

    //   }
    // }

    // const country = reactive({ props.chartData.countryCd: []})
  },
});
</script>

<style scoped lang="scss">
.chart-summary {
  width: 80%;
  height: 500px;
  padding: 50px 70px 52px;
  margin-bottom: 40px;
  box-shadow: 0 4px 24px 0 rgb(62 105 156 / 12%);
  background-color: #fff;
  border-radius: 16px;
}

.country-opt {
  margin-bottom: 40px;
  height: 500px;
  position: relative;
}

.option {
  padding: 24px 30px 80px;
  background: #f9fafc;
  display: flex;
  flex-direction: row;

  div {
    margin: 0 24px 10px 0;
  }
}

.country-all-filter {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  align-items: flex-start;

  .checkbox-all {
    margin: 0 !important;
    // position: relative;
    letter-spacing: 0.01em;
  }

  input {
    width: 15px;
    height: 15px;
    // position: absolute;
    border: solid 1px #8c8c8c;
    border-radius: 4px;
    vertical-align: top;
    background-color: #fff;
    margin: 2px 4px 0 0;
  }

  label {
    display: inline-block;
    color: #555;
    font-size: 10px;
    font-weight: normal;
    cursor: pointer;
  }
}

.country-filter {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  align-items: flex-start;

  .checkbox-country {
    // margin: 0 !important;
    margin-left: 10px;
    // position: relative;
    letter-spacing: 0.01em;
  }

  input {
    width: 15px;
    height: 15px;
    // position: absolute;
    border: solid 1px #8c8c8c;
    border-radius: 4px;
    vertical-align: top;
    background-color: #fff;
    margin: 2px 4px 0 0;
  }

  label {
    display: inline-block;
    color: #555;
    font-size: 10px;
    font-weight: normal;
    cursor: pointer;

    ::before {
      border-color: #00adef;
      background-color: #00adef;
    }

    ::after {
      opacity: 1;
    }
  }
}

.option-result {
  font-size: 14px;
  height: 360px;

  .count-total {
    position: relative;
    margin-top: 16px;
    padding: 0 0 25px;
    font-family: "actual", "Noto Sans KR";
    font-size: 12px;
    color: #222;
    border-bottom: 1px solid #bdbdbd;
    display: flex;
    align-items: center;
  }

  span {
    display: inline-block;
    margin-right: 31px;
    font-weight: bold;
  }

  strong {
    margin-left: 7px;
    font-size: 17px;
    color: #00adef;
    font-weight: 500;
  }
}
</style>
