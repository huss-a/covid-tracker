<template>
  <div class="w-full flex justify-center flex-col items-center my-20">
    <select
      name="country-select"
      class="w-80 bg-gray-300 rounded-lg px-5 py-1"
      @change="onChange($event)"
    >
      <option value="Global" :selected="isGlobal">Global</option>
      <option v-for="country in countries" :key="country.Country">
        {{ country.Country }}
      </option>
    </select>
    <div class="flex justify-center items-center mt-2">
      <button
        v-if="!isGlobal"
        class="text-md bg-red-600 px-3 py-1 rounded-full text-white mx-2"
        @click="selectGlobal()"
      >
        Clear Selection
      </button>
      <button
        v-if="hasChangedSelectionOnce"
        class="bg-red-600 px-3 py-1 rounded-full text-white mx-2"
        @click="updateData()"
      >
        Update Data
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CountrySelector",
  data() {
    return { isGlobal: true, hasChangedSelectionOnce: false };
  },
  props: ["countries"],
  methods: {
    onChange(e) {
      // console.log(e.target.value);
      this.$emit("country-change", e.target.value);
      this.isGlobal = e.target.value === "Global";
      if (!this.hasChangedSelectionOnce) this.hasChangedSelectionOnce = true;
    },
    selectGlobal() {
      this.isGlobal = true;
      this.$emit("country-change", "Global");
    },
    updateData() {
      this.$emit("refetch-data");
    },
  },
};
</script>
