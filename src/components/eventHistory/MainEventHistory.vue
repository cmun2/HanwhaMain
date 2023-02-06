<template>
  <div class="event-container">
    <div class="subject">Event History</div>
    <div class="event-total">
      <div
        class="event-box"
        :value="index"
        :key="index"
        v-for="(event, index) in dateMap"
        :event="event"
      >
        <div class="event-history">
          <div class="event-title">Serial No.</div>
          <div class="event-first">
            <div class="event-data">{{ event.deviceId }}</div>
            <span v-if="event.newFlag === 'Y'">New</span>
          </div>
        </div>
        <div class="event-history">
          <div class="event-title">Event Category</div>
          <div class="event-data">{{ event.eventCategory }}</div>
        </div>
        <div class="event-history">
          <div class="event-title">Start Date</div>
          <div class="event-data">{{ event.createDt }}</div>
        </div>
        <div class="event-history">
          <div class="event-title">Event Code</div>
          <div class="event-data">{{ event.eventCode }}</div>
        </div>
      </div>
    </div>
    <!-- <img src="../../../src/assets/right-arrow.png" alt="right-arrow" /> -->
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import moment from "moment";
export default defineComponent({
  name: "MainEventHistory",
  components: {},
  props: {
    eventData: {
      type: Object,
      default: () => {
        return;
      },
    },
  },
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  setup(props) {
    const dateMap = props.eventData.map((data: any) => {
      data.createDt = moment(data.createDt).format("DD[/]MM[/]YYYY h:mm");
      // const newDate = moment(data.createDt).format("DD[/]MM[/]YYYY h:mm");
      return data;
    });

    // const momentMap = props.eventData.filter((momentData: any) => {
    //   momentData.createDt(...momentData.createDt, dateMap);
    //   return momentData;
    // });

    // const momentMap

    return { dateMap };

    // props.eventData.replace();
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
.event-container {
  width: 50%;
  position: relative;
  box-shadow: 0 4px 24px 0 rgb(62 105 156 / 12%);
  border-radius: 16px;
  // background-color: #ffffff;

  // img {
  //   width: 15px;
  //   height: 15px;
  // }
}

.subject {
  padding: 30px 120px 20px;
  font-family: "actual", "Noto Sans KR";
  font-size: 20px;
  font-weight: 550;
  background-color: rgba(226, 230, 239, 0.5);
  color: #222;
  border-radius: 16px 16px 0 0;
}

.event-total {
  display: flex;
  flex-direction: column;
}

.event-box {
  padding: 20px 14px 29px;
}

.event-history {
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

.event-title {
  width: 179px;
  padding: 0 60px 0 9px;
  color: #555;
  box-sizing: border-box;
}

.event-first {
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
    color: #fff;
    border-radius: 2px;
    background-color: #00adef;
    vertical-align: middle;
    letter-spacing: 0;
  }
}

.event-data {
  color: #000;
  font-weight: 400;
}
</style>
