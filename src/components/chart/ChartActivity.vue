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
            <strong v-else>{{ totalproductCount.arrayProductCount }}</strong>
          </span>
          <span
            >Installed Last Week
            <strong v-if="allChecked === true">{{ sumAllLastWeek }}</strong>
            <strong v-else>{{ totalinstallCount.arrayInstallCount }}</strong>
          </span>
          <!-- <span>check: {{ sumCountry }}</span> -->
        </div>
        <PieGraph
          :normalOn="totalonlineNormalCount.arrayOnNormalCount"
          :warningOn="totalonlineWarningCount.arrayOnWarningCount"
          :errorOn="totalonlineErrorCount.arrayOnErrorCount"
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
    const onlineNormalCount: any = props.chartData.map((list: any) => {
      return list.onlineNormalCount;
    });
    const onlineWarningCount: any = props.chartData.map((list: any) => {
      return list.onlineWarningCount;
    });
    const onlineErrorCount: any = props.chartData.map((list: any) => {
      return list.onlineErrorCount;
    });
    const offlineNormalCount: any = props.chartData.map((list: any) => {
      return list.totalCount;
    });
    const offlineWarningCount: any = props.chartData.map((list: any) => {
      return list.offlineWarningCount;
    });
    const offlineErrorCount: any = props.chartData.map((list: any) => {
      return list.offlineErrorCount;
    });
    const offlineIncompleteCount: any = props.chartData.map((list: any) => {
      return list.offlineIncompleteCount;
    });

    const checkedCountry: Ref<string[]> = ref([]);
    const allChecked = ref(true);
    const allCount = reactive({ total: [] });

    //????????? ?????? ?????? ????????? ?????? function
    let sumAllCount: number = totalCount.reduce(
      (a: number, b: number) => a + b
    );

    let sumAllLastWeek: number = lastWeekCount.reduce(
      (a: number, b: number) => a + b
    );

    const sumArrayCount = (arr: number[]) =>
      arr.reduce((a: number, b: number) => a + b, 0);

    const arrayProductCount = sumArrayCount(totalCount);
    const arrayInstallCount = sumArrayCount(lastWeekCount);
    const arrayOnNormalCount = sumArrayCount(onlineNormalCount);
    const arrayOnWarningCount = sumArrayCount(onlineWarningCount);
    const arrayOnErrorCount = sumArrayCount(onlineErrorCount);

    const totalproductCount = reactive({
      arrayProductCount: arrayProductCount,
    });
    const totalinstallCount = reactive({
      arrayInstallCount: arrayInstallCount,
    });
    const totalonlineNormalCount = reactive({
      arrayOnNormalCount: arrayOnNormalCount,
    });
    const totalonlineWarningCount = reactive({
      arrayOnWarningCount: arrayOnWarningCount,
    });
    const totalonlineErrorCount = reactive({
      arrayOnErrorCount: arrayOnErrorCount,
    });

    // const sumArrayCount: number = totalCount.reduce((a: number, b: number) => a + b, 0)

    //countryCd??? ????????? checkedCountry.value??? ???????????? ?????? ????????? ?????????????????? totalCount??? ???

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
        totalproductCount.arrayProductCount = 0;
        totalinstallCount.arrayInstallCount = 0;
        totalonlineNormalCount.arrayOnNormalCount = 0;
        totalonlineWarningCount.arrayOnWarningCount = 0;
        totalonlineErrorCount.arrayOnErrorCount = 0;
      }
    };

    const countryClick = () => {
      if (checkedCountry.value.length === countryList.length) {
        allChecked.value = true;
      } else {
        allChecked.value = false;
        totalproductCount.arrayProductCount = 0;
        totalinstallCount.arrayInstallCount = 0;
        totalonlineNormalCount.arrayOnNormalCount = 0;
        totalonlineWarningCount.arrayOnWarningCount = 0;
        totalonlineErrorCount.arrayOnErrorCount = 0;
      }

      allCount.total = props.chartData.map((item: any) => {
        if (checkedCountry.value.includes(item.countryCd)) {
          totalproductCount.arrayProductCount += item.totalCount;
          totalinstallCount.arrayInstallCount += item.lastWeekCount;
          totalonlineNormalCount.arrayOnNormalCount += item.onlineNormalCount;
          totalonlineWarningCount.arrayOnWarningCount +=
            item.onlineWarningCount;
          totalonlineErrorCount.arrayOnErrorCount += item.onlineErrorCount;
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
      totalonlineNormalCount,
      totalonlineWarningCount,
      totalonlineErrorCount,
      totalinstallCount,
      totalproductCount,
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
  box-sizing: border-box;

  .count-total {
    position: relative;
    margin-top: 30px;
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
