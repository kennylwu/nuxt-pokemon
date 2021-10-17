<template>
    <div class="d-flex justify-content-center align-items-center pt-4">
        <form @submit="searchPokemon">
            <label id="search-label" for="find" class="d-block text-center text-white font-weight-bold">Find a Pokemon</label>
            <input id="find" type="text" class="d-block mx-auto form-control mb-2" v-model="search">
            <button id="go-btn" class="d-block mx-auto" type="submit">Go</button>
        </form>
    </div>
</template>

<script>

export default {
    data () {
        return {
            // index: [],
            search: '',
            results: [],
            show: false
        }
    },
    // computed: {
    //     async getPokemon() {
    //         await this.$axios.$get('https://pokeapi.co/api/v2/pokemon?limit=50')
    //         .then((res) => {
    //             this.show = true
    //             this.index = res.results;
    //         })
    //         .catch(console.log)
    //     }
    // },
    methods: {
        searchPokemon(evt){
            evt.preventDefault()

            // const index = Object.entries(this.index.results);
            const index = JSON.parse(JSON.stringify(this.index))

            console.log(index)
            // this.results = index.filter(([key, value]) => value.name == "bulbasaur")
            // console.log('search', this.results)
        }
    }
}
</script>


<style scoped>
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
</style>