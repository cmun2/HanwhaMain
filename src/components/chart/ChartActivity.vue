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
        <!-- <span>check: {{ totalCount }}</span> -->
        <!-- <span>check: {{ checkedCountry }}</span>
        <span>check: {{ allChecked }}</span> -->
      </div>
      <div class="option-result">
        <div class="count-total">
          <span
            >Product
            <strong v-if="allChecked === true">{{ sumAllCount }}</strong>
            <strong v-else>{{ totalproductCount.arrayCount }}</strong>
          </span>
          <span
            >Installed Last Week
            <strong v-if="allChecked === true">{{ sumAllLastWeek }}</strong>
            <strong v-else>{{ totalinstallCount.arrayCount }}</strong>
          </span>
          <!-- <span>check: {{ sumCountry }}</span> -->
        </div>
        <PieGraph
          :totalCount="totalCount"
          :lastWeekCount="lastWeekCount"
          :onlineNormalCount="onlineNormalCount"
          :onlineWarningCount="onlineWarningCount"
          :onlineErrorCount="onlineErrorCount"
          :offlineNormalCount="offlineNormalCount"
          :offlineWarningCount="offlineWarningCount"
          :offlineErrorCount="offlineErrorCount"
          :offlineIncompleteCount="offlineIncompleteCount"
          :chartData="chartData"
        />
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, watch, ref, Ref, computed } from "vue";
import PieGraph from "./PieGraph.vue";

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

  setup(props, { emit }) {
    const countryList: string = props.chartData.map((list: any) => {
      return list.countryCd;
    });

    const totalCount: any = props.chartData.map((list: any) => {
      return list.totalCount;
    });
    const lastWeekCount: any = props.chartData.map((list: any) => {
      return list.lastWeekCount;
    });
    const onlineNormalCount: number = props.chartData.map((list: any) => {
      return list.onlineNormalCount;
    });
    const onlineWarningCount: number = props.chartData.map((list: any) => {
      return list.onlineWarningCount;
    });
    const onlineErrorCount: number = props.chartData.map((list: any) => {
      return list.onlineErrorCount;
    });
    const offlineNormalCount: number = props.chartData.map((list: any) => {
      return list.totalCount;
    });
    const offlineWarningCount: number = props.chartData.map((list: any) => {
      return list.offlineWarningCount;
    });
    const offlineErrorCount: number = props.chartData.map((list: any) => {
      return list.offlineErrorCount;
    });
    const offlineIncompleteCount: number = props.chartData.map((list: any) => {
      return list.offlineIncompleteCount;
    });

    const checkedCountry: Ref<string[]> = ref([]);
    const allChecked = ref(true);
    const allCount = reactive({ total: [] });

    //배열로 뽑은 값을 더하기 위한 function
    let sumAllCount: number = totalCount.reduce(
      (a: number, b: number) => a + b
    );

    let sumAllLastWeek: number = lastWeekCount.reduce(
      (a: number, b: number) => a + b
    );

    const sumArrayCount = (arr: number[]) =>
      arr.reduce((a: number, b: number) => a + b, 0);

    const arrayCount = sumArrayCount(totalCount);
    const totalproductCount = reactive({ arrayCount: arrayCount });
    const totalinstallCount = reactive({ arrayCount: arrayCount });

    // const sumArrayCount: number = totalCount.reduce((a: number, b: number) => a + b, 0)

    //countryCd의 나라와 checkedCountry.value와 비교하여 같은 경우의 데이터파일의 totalCount의 합

    // let sumCountry: number = props.chartData
    //   .filter(
    //     (item: { countryCd: any }) => item.countryCd === checkedCountry.value
    //   )
    //   .reduce((a: number, b: number) => a + b, 0);
    // console.log(props.chartData.countryCd);

    for (let i = 0; i < countryList.length; i++) {
      checkedCountry.value.push(countryList[i]);
    }

    const allClick = () => {
      if (!allChecked.value) {
        if (checkedCountry.value.length != 0) {
          checkedCountry.value = [];
        }
        for (let i = 0; i < countryList.length; i++) {
          checkedCountry.value.push(countryList[i]);
        }
        allChecked.value = true;
      } else {
        checkedCountry.value = [];
        allChecked.value = false;
        totalproductCount.arrayCount = 0;
        totalinstallCount.arrayCount = 0;
      }
    };

    const countryClick = () => {
      if (checkedCountry.value.length === countryList.length) {
        allChecked.value = true;
      } else {
        allChecked.value = false;
        totalproductCount.arrayCount = 0;
        totalinstallCount.arrayCount = 0;
      }

      allCount.total = props.chartData.map((item: any) => {
        if (checkedCountry.value.includes(item.countryCd)) {
          totalproductCount.arrayCount += item.totalCount;
          totalinstallCount.arrayCount += item.lastWeekCount;
        }
      });
    };

    const selectedCountry = reactive(
      computed(() => {
        return emit("checkedCountry", checkedCountry.value);
      })
    );
    // const countTotalValue = (checkedCountries: string[]) => {
    //   console.log("check", checkedCountries);
    // };

    // const countTotalValue = () => {
    //   allCount.total = props.chartData.map((item: any) => {
    //     if (checkedCountry.value.includes(item.countryCd)) {
    //       totalproductCount.arrayCount += item.totalCount;
    //     }
    //   });
    // };

    return {
      totalinstallCount,
      totalproductCount,
      arrayCount,
      sumAllCount,
      sumAllLastWeek,
      allClick,
      allChecked,
      checkedCountry,
      selectedCountry,
      countryClick,
      totalCount,
      lastWeekCount,
      onlineNormalCount,
      onlineWarningCount,
      onlineErrorCount,
      offlineNormalCount,
      offlineWarningCount,
      offlineErrorCount,
      offlineIncompleteCount,
    };
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
  padding: 24px 20px 5px;
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
