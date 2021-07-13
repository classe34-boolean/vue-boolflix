<template>
  <div id="app">
    <Header @performSearch="search"/>

    <Main 
      :movieCards="movies"
      :serieCards="series"
      :searching="searchStarted"
      />
  </div>
</template>

<script>
import axios from 'axios';

import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main
  },
  data: function() {
     return {
       apiUrl: 'https://api.themoviedb.org/3/search/',
       apiKey: 'e99307154c6dfb0b4750f6603256716d',
       movies: [],
       series: [],
       allResults: [],
       searchStarted: false
     }   
  },
  computed: {
    computedResults: function() {
      return [...this.movies, ...this.series];
    }
  },
  methods: {
    getMovies: function(obj) {
      axios
        .get(this.apiUrl + 'movie', obj)
        .then(
          (res) => {
            // console.log(res);
            this.movies = res.data.results;
            this.allResults = [...this.series, ...this.movies];
            this.searchStarted = true;
          }
        )
        .catch(
          (err) => {
            console.log("Errore", err);
          }
        );
    },
    getSeries: function(obj) {
      axios 
        .get(this.apiUrl + 'tv', obj)
        .then(
          (res) => {
            // console.log(res.data);
            this.series = res.data.results;
            this.allResults = [...this.movies, ...this.series];
            this.searchStarted = true;
          }
        )
        .catch(
          (err) => {
            console.log("Errore", err);
          }
        );
    },

    search: function(text) {

      const paramsObj = {
          params: {
            api_key: this.apiKey,
            query: text,
            language: 'it-IT'
          }
        };
        
        this.getMovies(paramsObj);
        this.getSeries(paramsObj);
    }
  }
}
</script>

<style lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.min.css';

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
</style>
