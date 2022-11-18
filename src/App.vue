<template>
  <beer-info v-if="beers.length>0" :beers="beers" class="main-container"></beer-info>
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
      beers: []
    }
  },
  mounted() {
   const response = this.getUser();
    response.then(res => { this.beers = res.data})
  },
  methods: {
     async getUser() {
     return await axios.get('https://api.punkapi.com/v2/beers?brewed_before=11-2012&abv_gt=6');
    }
  }
}
</script>

<style>
.main-container {
  font-family: system-ui;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #2c3e50;
}
</style>
