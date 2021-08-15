<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <CountrySelect @get-country="getCountryData" :countries="countries" />
    <div class="text-center">
      <button
        @click="clearCountryData"
        class="bg-green-500 text-white rounded py-2 px-4 my-4 hover:bg-green-600"
      >
        Clear Country
      </button>
    </div>
    <DataBoxes :stats="stats" />
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-blue-800 text-4xl font-semibold mt-8 mb-5 ">
      Fetching Data...
    </div>
    <img :src="loadingImage" class="w-20 m-auto" alt="loading.gif" />
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle";
import DataBoxes from "@/components/DataBoxes";
import CountrySelect from "@/components/CountrySelect";

export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/loading.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.title = "Global";
      this.stats = data.Global;
      this.loading = false;
    },
  },
  async created() {
    const data = await this.fetchCovidData();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
