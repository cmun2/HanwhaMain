<template>
  <div class="chart-summary">
    <div class="country-opt">
      <div class="country-filter"></div>
    </div>
    <PieGraph />
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import PieGraph from "./PieGraph.vue";
export default defineComponent({
  components: { PieGraph },
  data() {
    return {
      sampleData: "",
    };
  },
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  setup() {},
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
.chart-summary {
  width: 80%;
  height: 500px;
  padding: 50px 70px 52px;
  margin-bottom: 40px;
  box-shadow: 0 4px 24px 0 rgb(62 105 156 / 12%);
  background-color: #fff;
  border-radius: 16px;
}
</style>
