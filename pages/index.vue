<template>
  <div id="main">
    <Header/>

    <div class="d-flex justify-content-center align-items-center pt-4">
      <span v-if="!show" class="text-white">Loading...</span>
      <form @submit="searchPokemon" v-if="show">
          <label id="search-label" for="find" class="d-block text-center text-white font-weight-bold">Find a Pokemon</label>
          <input id="find" type="text" class="d-block mx-auto form-control mb-2" v-model="search">
          <button id="go-btn" class="d-block mx-auto" type="submit">Go</button>
      </form>
      <b-modal ref="results-modal" hide-footer centered>
      <div class="d-block">
        <p v-if="results.length <= 0" class="text-danger">Error: No Pokémons found</p>
        <ul v-if="results.length > 0" class="text-danger">
          <li v-for="(item, key) in results" :key="key">{{ item.name }}</li>
        </ul>
      </div>
    </b-modal>
    </div>

    <Carousel/>
  </div>
</template>

<script>
export default {
  data () {
        return {
            index: [],
            search: '',
            results: [],
            show: false
        }
    },
    computed: {
        async getPokemon() {
            await this.$axios.$get('https://pokeapi.co/api/v2/pokemon?limit=50')
            .then((res) => {
                this.show = true
                this.index = res.results;
            })
            .catch(console.log)
        }
    },
     methods: {
        searchPokemon(evt){
            evt.preventDefault()
            const index = JSON.parse(JSON.stringify(this.index))
            this.results = index.filter((value) => value.name.includes(this.search.toLowerCase()))
            this.$refs['results-modal'].show()
            console.log('search', this.results)
        }
    }
}
</script>

<style>
#main {
  background: linear-gradient(#00A1FC, #054C74);
  height: 100vh;
}
.carousel-indicators {
    bottom: -60px !important;
}
#search-label {
    font-size: 30px;
}
#go-btn {
    height: 60px;
    width: 105px;
    left: 0px;
    top: 0px;
    border-radius: 30px;
    background: #FFCB05;
    color:#BF3636;
    font-size: 30px;
    font-weight: 700;
    border-width: 0;
}
.modal-content {
  background: #FFCB05;
}
.modal-header {
  border-bottom: 0;
}
</style>