<template>
  <div class="home">
    <div class="container">
      <MainHeader />
      <div class="page-content">
        <div class="page-container">
          <div class="chart-summary">
            <ChartActivity />
          </div>
          <div class="prod-summary">
            <MainEventHistory />
            <MainRecentActivity />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ChartActivity from "../components/chart/ChartActivity.vue";
import MainEventHistory from "../components/eventHistory/MainEventHistory.vue";
import MainHeader from "../components/header/MainHeader.vue";
import MainRecentActivity from "../components/recentActivity/MainRecentActivity.vue";

export default defineComponent({
  name: "HomeView",
  components: {
    MainEventHistory,
    MainHeader,
    MainRecentActivity,
    ChartActivity,
  },
});
</script>

<style scoped lang="scss">
.container {
  width: 100%;
  height: 100%;
  font-size: 16px;
}
</style>
