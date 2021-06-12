<template>
  <div class="text-center">
    <h2 class="font-bold text-2xl sm:text-3xl">
      {{ title }}
    </h2>
    <div class="text-1xl sm:text-2xl mt-4 tb-10">
      {{ timestamp }}
    </div>
  </div>
</template>

<script>
import dayjs from "dayjs";

export default {
  props: ["title", "dataDate"],
  computed: {
    timestamp: function() {
      return dayjs(this.dataDate).format("MMMM D YYYY (dddd), h:mm:ss a");
    },
  },
  created() {
    console.log(this.timestamp);
  },
};
</script>
