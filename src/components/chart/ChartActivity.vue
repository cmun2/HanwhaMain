<template>
  <div>
    <div></div>
    <PieGraph />
  </div>
</template>
<script>
import PieGraph from "./PieGraph.vue";
export default {
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
};
</script>
