<template>
  <div class="header_space">
    <div class="logo">LOGO</div>
    <div class="search_space">
      <input
        type="text"
        id="content_search"
        name="content_search"
        placeholder="Effettua una ricerca"
        v-model="searchValue"
        @keyup.enter="startSearch()"
      />
      <button @click="startSearch()">Cerca</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'MyHeader',
  data() {
    return {
      searchValue: '',
      //   array che contiene risposta alla ricerca filtrata da input
      resultArray: [],
      movieResultArray: [],
      seriesResultArray: [],
      apiLinkRoot: 'https://api.themoviedb.org/3/search/',
      apiLinkMovie: 'movie?',
      apiLinkSeries: 'tv?',
      apiLinkKey: 'api_key=8c2a59c90f2e8f4d2da84becf8da96e9&',
      apiLinkLanguage: 'language=it-IT&',
      apiLinkEnd: 'page=1&include_adult=false&',
      apiLinkQuery: 'query=',
    };
  },
  methods: {
    startSearch() {
      axios
        //   chiamata per i film
        .get(
          this.apiLinkRoot +
            this.apiLinkMovie +
            this.apiLinkKey +
            this.apiLinkLanguage +
            this.apiLinkEnd +
            this.apiLinkQuery +
            this.searchValue.replace(/\s+/g, '+')
        )
        .then((response) => {
          const firstResult = response.data.results;
          this.movieResultArray = firstResult;
          this.$emit('filteredMovieSearch', this.movieResultArray);
        })
        .catch((error) => {
          console.log('Errore', error);
        });
      //   chiamata per serie tv
      axios
        .get(
          this.apiLinkRoot +
            this.apiLinkSeries +
            this.apiLinkEnd +
            this.apiLinkKey +
            this.apiLinkLanguage +
            this.apiLinkQuery +
            this.searchValue.replace(/\s+/g, '+')
        )
        .then((response) => {
          const secondResult = response.data.results;
          this.seriesResultArray = secondResult;
          this.$emit('filteredSeriesSearch', this.seriesResultArray);
        })
        .catch((error) => {
          console.log('Errore', error);
        });
    },
  },
};
</script>

<style lang="scss" scoped>
.header_space {
  background-color: lightsalmon;
  display: flex;
  padding: 10px;
}
.logo {
  width: 50%;
}
.search_space {
  width: 50%;
  display: flex;
  justify-content: end;
  align-content: center;
}
</style>
