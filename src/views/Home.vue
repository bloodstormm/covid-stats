<template>
  <main class="bg-gray-100 dark:bg-gray-900 dark:text-gray-100 min-h-screen pt-4" v-if="!loading">
      <DataTitle :text="title" :date="date" :status="status" />

      <CountrySelect @get-country="getCountryData" :countries="countries" />

      <DataBoxes :status="status" />

      <!-- Reset Global button -->
      <div class="flex justify-center">
        <button
          @click='resetGlobal()'
          v-if='status.Country'
          class="bg-green-600 text-center text-white rounded-lg shadow-xl mt-2 focus:outline-none hover:bg-green-700 p-3"
        >
          Voltar ao Global
        </button>
      </div>
    </main>

    <!-- Loading Page -->
    <main class="bg-gray-100 dark:bg-gray-800 min-h-screen flex flex-col text-center" v-else>
      <div>
        <h1 class="text-3xl m-10 font-semibold text-green-600">Carregando os dados</h1>
      </div>
      <img :src="loadingImg" alt="Loading circle" class="h-28 mx-auto" />
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
      date: "",
      status: {},
      countries: [],
      loadingImg: require("../assets/loading.gif"),
    };
  },
  methods: {
    // Capturando os dados da API
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();

      return data;
    },

    getCountryData(country) {
      this.status = country;
      this.title = country.Country;
    },

    async resetGlobal() {
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = 'Global'
      this.status = data.Global
      this.loading = false
    }
  },
  async created() {
    const data = await this.fetchCovidData();

    this.date = data.Date,
    this.status = data.Global,
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
