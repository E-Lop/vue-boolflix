<template>
  <div id="app">
    <MyHeader
      @filteredMovieSearch="showMovieFilteredResults"
      @filteredSeriesSearch="showSeriesFilteredResults"
    />

    <MyDBList
      :receivedMovieResults="movieResultsToDisplay"
      :receivedSeriesResults="movieResultsToDisplay"
    />
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue';
import MyDBList from './components/MyDBList.vue';

export default {
  name: 'App',
  components: {
    MyHeader,
    MyDBList,
  },
  data() {
    return {
      // array ricevuto tramite emit
      movieResultsToDisplay: [],
      seriesResultsToDisplay: [],
    };
  },
  methods: {
    showMovieFilteredResults(resultArray) {
      this.movieResultsToDisplay = resultArray;
    },
    showSeriesFilteredResults(resultArray) {
      this.seriesResultsToDisplay = resultArray;
    },
  },
};
</script>

<style lang="scss">
@import './assets/style/common.scss';
</style>
