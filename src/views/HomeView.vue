<template>
  <div class="home">
    <div class="container">
      <MainHeader />
      <div class="page-content">
        <div class="page-container">
          <ChartActivity :chartData="chartData" />
          <div class="prod-summary">
            <MainEventHistory :eventData="eventData" />
            <MainRecentActivity :activityData="activityData" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed } from "vue";
import ChartActivity from "../components/chart/ChartActivity.vue";
import MainEventHistory from "../components/eventHistory/MainEventHistory.vue";
import MainHeader from "../components/header/MainHeader.vue";
import MainRecentActivity from "../components/recentActivity/MainRecentActivity.vue";
import JsonFile from "../components/sample/data.json";

export default defineComponent({
  name: "HomeView",
  components: {
    MainEventHistory,
    MainHeader,
    MainRecentActivity,
    ChartActivity,
  },

  setup() {
    const chartData = JsonFile.chart.map((lists: object) => {
      return lists;
    });

    const eventData = JsonFile.event.map((lists: object) => {
      return lists;
    });
    const activityData = JsonFile.activity.map((lists: object) => {
      return lists;
    });
    return {
      chartData,
      eventData,
      activityData,
    };
  },
});
</script>

<style scoped lang="scss">
.home {
  width: 100%;
  height: 100%;
}
.container {
  min-height: 100%;
  width: 100%;
  min-width: 1200px;
}

.page-content {
  width: 100%;
  position: relative;
}

.page-container {
  margin-left: auto;
  margin-right: auto;
  max-width: 1600px;
  margin-top: 20px;
  padding: 40px 50px 144px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.prod-summary {
  display: flex;
  justify-content: space-between;
  width: 92%;
}
</style>
