<template>
  <div class="grid md:grid-cols-2 gap-4 mt-4">
    <div class="data-box">
      <!-- cases box -->
      <h3 class="text-3xl font-bold mb-4 text-red-900">
        Cases
      </h3>
      <h5 class="text-center text-2xl font-bold">
        Total:
        <span class="font-semibold">{{
          addCommasToNumber(stats.TotalConfirmed)
        }}</span>
      </h5>
      <h5 class="text-center text-2xl font-bold">
        New:
        <span class="font-semibold">{{
          addCommasToNumber(stats.NewConfirmed)
        }}</span>
      </h5>
    </div>
    <div class="data-box">
      <!-- deaths box -->
      <h3 class="text-3xl font-bold mb-4 text-red-900">
        Deaths
      </h3>
      <h5 class="text-center text-2xl font-bold">
        Total:
        <span class="font-semibold">{{
          addCommasToNumber(stats.TotalDeaths)
        }}</span>
      </h5>
      <h5 class="text-center text-2xl font-bold">
        New:
        <span class="font-semibold">{{
          addCommasToNumber(stats.NewDeaths)
        }}</span>
      </h5>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataBoxes",
  props: ["stats"],
  computed: {
    stringifiedJson: function() {
      return JSON.stringify(this.stats);
    },
  },
  methods: {
    addCommasToNumber: function(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },
};
</script>

<style scoped>
.data-box {
  @apply shadow-md bg-red-200 p-10 text-center rounded-md;
}
</style>
