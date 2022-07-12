<template>
  <div id="app">
    <MyHeader @filteredSearch="showFilteredResults" />
    <MyDBList :receivedResults="resultsToDisplay" />
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
      resultsToDisplay: [],
    };
  },
  methods: {
    showFilteredResults(resultArray) {
      this.resultsToDisplay = resultArray;
    },
  },
};
</script>

<style lang="scss">
@import './assets/style/common.scss';
</style>
