<template>
  <div class="main-container">
    <b-form-input v-model.trim="beerName" placeholder="Search by Beer name"></b-form-input>
  <div class="beer-info-container" v-for="beer in filteredBeers" :key="beer.id">

    <div>
      <img class="beer-image" :src=beer.image_url>
    </div>

    <div class="beer-info">
      <h1>{{beer.name}}</h1>
      <h3>{{beer.tagline}}</h3>
      <h4 class="description">Description: {{beer.description}}</h4>
      <h4>Tips:{{beer.brewers_tips}}</h4>

      <h4>Food Pairings:</h4>
      <div>
        <ul>
          <li v-for="foodPairing in beer.food_pairing" :key="foodPairing">
            {{foodPairing}}
          </li>
        </ul>
      </div>
    </div>

  </div>
  </div>
</template>

<script>
export default {
  name:"BeerInfo",
  props: {
    beers: Array
  },
  data() {
    return {
      beerName: '',
      bottom: false,
    }
  },
  watch: {
    bottom(newValue) {
      if (newValue) {
        this.$emit('loadMoreBeers')
      }
    }
  },
  mounted() {
    window.addEventListener("scroll", () => {
      this.bottom = this.bottomVisible();
    });
  },
  computed: {
    filteredBeers(){
      console.log(this.beers)
      if(!this.beerName) return this.beers;

      const name = this.beerName.toUpperCase();
      return this.beers.filter(beer => beer.name.startsWith(name) || beer.name.includes(name))
    }
  },
  methods: {
    bottomVisible() {
      const scrollY = window.scrollY;
      const visible = document.documentElement.clientHeight;
      const pageHeight = document.documentElement.scrollHeight;
      const bottomOfPage = visible + scrollY >= pageHeight;
      return bottomOfPage || pageHeight < visible;
    },
  }
}
</script>

<style lang="css" scoped>
.main-container {
  margin-left:30%;
  margin-right:30%;

  text-align: center;
  margin-top: 60px;
}

.beer-info-container {
  display: flex;
  height:500px;
  margin-top: 50px;
  background-color: red;
}

.beer-image {
  margin-left: 20px;
  margin-top: 20px;
  margin-right: 20px;
  height: 93%;
  width: 150px;
}

.beer-info {
  width: calc(100% - 150px);
  padding: 60px 20px 60px 20px;
  background-color: olive;
  color: white;
  text-align: left;
}

.description {
  max-height: 50px;
  height: 50px;
  overflow: auto;
  text-overflow: ellipsis;
}
</style>
