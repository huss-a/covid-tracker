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
  <main class="flex justify-center items-center w-full h-full" v-else>
    <Spinner spinnerColor="red" />
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle";
import DataBoxes from "@/components/DataBoxes";
import CountrySelector from "@/components/CountrySelector";
import About from "@/components/About";
import Spinner from "@/components/Spinner";

export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelector,
    About,
    Spinner,
  },
  data() {
    return {
      stats: {},
      loading: true,
      global: {},
      countries: [],
      title: "Global",
      dataDate: "",
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
      this.title = country;
      if (country === "Global") {
        this.stats = this.global;
      } else {
        this.stats = this.countries.find((c) => c.Country === country);
      }
    },
  },
};
</script>
