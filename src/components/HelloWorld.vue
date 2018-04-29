<template>
  <div class="hello">

    <input @keyup.enter="search" v-model="q">
    <button @click="search">Search</button>
    <hr>
   <div v-if="movie.Poster !== 'N/A'"  v-for="movie in movies" :key="movie.imdbID" class="poster">
   
   <img :src="movie.Poster" :alt="movie.Title">
   </div>
  </div>
</template>

<script>
// import axios from 'axios'
import {mapActions, mapGetters} from 'vuex'

export default {
  name: 'HelloWorld',
  data () {
    return {
     q: 'avenger'
    }
  },
  computed: {
    ...mapGetters(['movies'])
  },
  async created () {
    this.fetchMovies(this.q)
  //  let movies = await axios.get('http://www.omdbapi.com/?s=avenger&apikey=409a3997')
  //  this.movies = movies.data.Search
  },
  methods: {
    ...mapActions(['fetchMovies']),
    search () {
      this.fetchMovies(this.q)
    }
    // async search () {
    // let movies = await axios.get('http://www.omdbapi.com/?s='+this.q+'&apikey=409a3997')
    // this.movies = movies.data.Search
    // }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.poster {
  display: inline-block;
}
img {
  width: 240px;
}
</style>
