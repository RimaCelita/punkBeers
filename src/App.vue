<template>
  <beer-info v-if="beers.length>0"
             :beers="beers"
             @loadMoreBeers="loadMoreBeers()">
  </beer-info>
</template>

<script>
import BeerInfo from './components/BeerInfo'
const axios = require('axios').default;
export default {
  name: 'App',
  components: {
    BeerInfo
  },
  data(){
    return {
      beers: [],
      page:1,
      ipp:80,  // 1 to 80
      totalItems: 325 // first 4 pages -> 80 + 5th page 5 items
    }
  },
  mounted() {
   const response = this.getBeers(this.page);
    response.then(res => { this.beers = res.data})
  },
  methods: {
     async getBeers(page) {
     return await axios.get(`https://api.punkapi.com/v2/beers?page=${page}&per_page=${this.ipp}`);
    },
    loadMoreBeers() {
      this.page++;
     if(Math.ceil(
         this.totalItems /(this.page * this.ipp)) > 1){
       const response = this.getBeers(this.page);
       response.then(res => { this.beers.push(...res.data)})
     } else {
       console.log('no more beers to list!!')
     }


    }
  }
}
</script>
