<template>
  <main v-if="!loading">
  <DataTitle :text="title" :dataDate="dataDate" />
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>  
    <div class="text-gray-400 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" alt="
    w-24 m-auto" srcset="">
  </main>
</template>

<script>

import DataTitle from '@/components/DataTitle'
export default {
  name: 'Home',
  components: {
    DataTitle
  },
  data() {
  return {
    loading: true,
    title: 'Global',
    dataDate: '',
    stats: {},
    countries: [],
    loadingImage: require('../assets/hourglass.gif')
  }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary')
      const data = res.json()

      return data;
    }
  },
 async  created() {
    const data = await this.fetchCovidData()
    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false

  }
}
</script>
