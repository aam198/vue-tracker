<template>
  <main v-if="!loading">
   <DataTitle :text="title" :dataDate="dataDate" />
   <DataBoxes :stats="stats" />
   <CountrySelect @get-country="getCountryData" :countries="countries" />

  <!-- Only shows if a Country is selected -->
   <button v-if="stats.Country" @click="clearCountryData" class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">Clear Country</button> 
  </main>
  <!-- If Data is not ready, the loader will show -->
  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-24 m-auto" alt="" />
  </main>
</template>

<script>
// @ is an alias to /src
import DataTitle from '@/components/DataTitle.vue';
import DataBoxes from '@/components/DataBoxes.vue';
import CountrySelect from '@/components/CountrySelect.vue';

export default {
  name: 'Home',
  components: { DataTitle, DataBoxes, DataBoxes, CountrySelect },
  data() {
    // return an object with our data, right now setting up what we will be returning i.e. an object, or an array etc.
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif'),
    }
  },
  methods: {
   async fetchCovidData() {
     const response = await fetch('https://api.covid19api.com/summary');
     const data = await response.json();
     return data;
    },
    getCountryData(country) {
      // stats will equal the country instead of Global
      this.stats = country;
      this.title = country.Country;
    },
    // Will re-fetch the data so need async
    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.title = 'Global';
      this.stats = data.Global;
      this.loading = false;
    }
  },
  // async since it is returning a promise
  async created() {
    const data = await this.fetchCovidData();
    console.log(data);
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  }
}
</script>
