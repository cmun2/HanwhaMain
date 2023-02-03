<template>
  <div class="activity-container">
    <div class="subject">Recent Activities</div>
    <div class="activity-total">
      <div
        class="activity-box"
        :value="index"
        :key="index"
        v-for="(activity, index) in activityData"
        :activity="activity"
      >
        <div class="activity-history">
          <div class="activity-title">Serial No.</div>
          <div class="activity-first">
            <div class="activity-data">{{ activity.deviceId }}</div>
            <span v-if="activity.activityType === 'Installation'"
              >Installation</span
            >
            <span v-else>Replacement</span>
          </div>
        </div>
        <div class="activity-history">
          <div class="activity-title">Date</div>
          <div class="activity-data">{{ activity.createDt }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "MainRecentActivity",
  components: {},
  props: {
    activityData: {
      type: Object,
      default: () => {
        return;
      },
    },
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
.activity-container {
  width: 50%;
  height: 100%;
  position: relative;
  box-shadow: 0 4px 24px 0 rgb(62 105 156 / 12%);
  border-radius: 16px;
  background-color: #ffffff;
  margin-left: 40px;
}

.subject {
  padding: 30px 120px 22px;
  font-family: "actual", "Noto Sans KR";
  font-size: 20px;
  font-weight: 550;
  background-color: rgba(226, 230, 239, 0.5);
  color: #222;
  border-radius: 16px 16px 0 0;
}

.activity-total {
  display: flex;
  flex-direction: column;
}

.activity-box {
  padding: 20px 14px 29px;
}

.activity-history {
  display: flex;
  flex-direction: row;

  div {
    overflow: hidden;
    font-family: "Rubik", "Noto Sans KR";
    font-size: 14px;
    line-height: 1.8;
    letter-spacing: 1px;
  }
}

.activity-title {
  width: 179px;
  padding: 0 60px 0 9px;
  color: #555;
  box-sizing: border-box;
}

.activity-first {
  width: calc(100% - 179px);
  display: flex;
  flex-direction: row;

  span {
    display: inline-block;
    font-size: 5px;
    font-family: "Rubik", "Noto Sans KR";
    font-weight: 500;
    margin-left: 8px;
    margin-top: 4px;
    padding: 1px 1px 0;
    color: #333;
    border-radius: 2px;
    background-color: #15dbb7;
    vertical-align: middle;
    letter-spacing: 0;
  }
}

.activity-data {
  color: #000;
  font-weight: 400;
}
</style>
