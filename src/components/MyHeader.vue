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
      apiLink:
        'https://api.themoviedb.org/3/search/movie?api_key=8c2a59c90f2e8f4d2da84becf8da96e9&language=en-US&page=1&include_adult=false&query=',
    };
  },
  methods: {
    startSearch() {
      axios
        //   il link è fatto da una radice fissa + input utente in cui spazi sostituiti da +
        .get(this.apiLink + this.searchValue.replace(/\s+/g, '+'))
        .then((response) => {
          const singleResult = response.data.results;
          this.resultArray = singleResult;
          console.log('array', this.resultArray);
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
