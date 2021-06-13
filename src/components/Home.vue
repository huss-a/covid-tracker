<template>
  <main v-if="!loading" class="font-rubik">
    <DataTitle :title="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
    <CountrySelector
      @country-change="updateData($event)"
      @refetch-data="refetchData()"
      :countries="countries"
    />
    <About />
  </main>
  <main class="flex justify-center items-center w-full" v-else>
    <img class="w-48" :src="loadingImage" alt="Loading..." />
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle";
import DataBoxes from "@/components/DataBoxes";
import CountrySelector from "@/components/CountrySelector";
import About from "@/components/About";

export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelector,
    About,
  },
  data() {
    return {
      stats: {},
      loading: true,
      global: {},
      countries: [],
      title: "Global",
      dataDate: "",
      loadingImage: require("@/assets/hourglass.gif"),
    };
  },
  async created() {
    const data = await this.fetchCovidData();
    this.stats = data.Global;
    this.global = data.Global;
    this.countries = data.Countries;
    this.dataDate = data.Date;
    this.loading = false;
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary").catch(
        console.error
      );
      const data = await res.json();
      return data;
    },
    async refetchData() {
      this.loading = true;
      const res = await fetch("https://api.covid19api.com/summary").catch(
        console.error
      );
      const data = await res.json();
      this.stats = data.Global;
      this.global = data.Global;
      this.title = "Global";
      this.countries = data.Countries;
      this.dataDate = data.Date;
      this.loading = false;
    },
    updateData(country) {
      if (country === "Global") {
        this.stats = this.global;
        this.title = country;
      } else {
        this.stats = this.countries.find((c) => c.Country === country);
        this.title = country;
      }
    },
  },
};
</script>
