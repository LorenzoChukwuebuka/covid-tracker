<template>
  <main v-if="!loading">
     <DataTitle :text="title" :dataDate="dataDate" />

     <DataBoxes :stats="stats" />

     <country @get-country="getCountryData" :countries="countries" />

      <button v-if="stats.Country" @click="clearCountryData" class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600"> Clear Country </button>


  </main>
   <main class="flex flex-col align-center justify-center text-center" v-else>

     <div class="text-gray-500 text-3xl mt-10 mb-6">
       fetching Data
     </div>
     <img :src="loadingImage" class="w-24 m-auto"/>
   </main>
</template>

<script>
 import axios from 'axios'
 import DataTitle from '../components/dataTitle.vue'
 import DataBoxes from '../components/dataBoxes.vue'
 import Country from '../components/countrySelect.vue'

export default {
  name: 'Home',
  components:{
    DataTitle,
    DataBoxes,
    Country
  },
  data(){
    return{
      loading:true,
      title:"Global",
      dataDate:'',
      stats:{},
      countries:[],
      loadingImage:require('../assets/tenor.gif')
    }
  },

  created(){
    this.fetchCovidData()
  },
  methods:{
    fetchCovidData(){
      axios.get("https://api.covid19api.com/summary")
      .then(res=>{
       this.dataDate = res.data.Date
       this.stats = res.data.Global
       this.countries= res.data.Countries
       this.loading = false
        
      })
    } ,

    getCountryData(country){
      this.stats = country
      this.title = country.Country
    },

     async clearCountryData(){
      this.loading = true
      const data = await this.fetchCovidData()
      this.title='Global'
      this.stats =  data.Global
      this.loading = false
    }

   }
   
}
</script>
