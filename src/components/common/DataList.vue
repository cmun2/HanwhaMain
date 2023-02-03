<template>
  <!-- <div class="list-container"> -->
  <!-- <span v-if="event">Serial No. {{ event.deviceId }}</span> -->
  <span>{{ event.deviceId }}</span>
  <!-- <span v-if="event">Event Category {{ event.eventCategory }}</span>
    <span v-if="event">Start Date {{ event.createDt }}</span>
    <span v-if="event">Event Code {{ event.eventCode }}</span> -->
  <!-- </div> -->
</template>

<script lang="ts">
import { defineComponent } from "vue";
// import moment from "moment";
export default defineComponent({
  name: "DataList",
  props: {
    eventData: {
      type: Object,
      default: () => {
        return;
      },
    },
    event: {
      type: Object,
      default: () => {
        return;
      },
    },
  },

  setup(props) {
    // console.log("1", props.eventData);
    // console.log(props.eventData);
    console.log("2", props.event);
    const state = {};

    return {
      state,
    };
  },
});
</script>

<style lang="scss" scoped>
.list-container {
  padding: 30px 120px 20px;

  .span {
    font-size: 12px;
  }
}
</style>
