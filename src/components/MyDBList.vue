<template>
  <div class="main-box">
    <div class="film" v-if="receivedMovieResults.length > 0">
      <h2>Film</h2>
      <ul>
        <li>
          <MyDBCard
            v-for="(movie, index) in receivedMovieResults"
            :key="index"
            :desiredMovieCards="receivedMovieResults[index]"
          />
        </li>
      </ul>
    </div>
    <div class="serie" v-if="receivedSeriesResults.length > 0">
      <h2>Serie TV</h2>
      <ul>
        <li>
          <MyDBCard
            v-for="(series, index) in receivedSeriesResults"
            :key="index"
            :desiredSeriesCards="receivedSeriesResults[index]"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import MyDBCard from './MyDBCard.vue';

export default {
  name: 'MyDBList',
  components: {
    MyDBCard,
  },
  data() {
    return {};
  },
  props: {
    receivedMovieResults: Array,
    receivedSeriesResults: Array,
  },
};
</script>

<style lang="scss" scoped>
.main-box {
  display: flex;
  flex-wrap: wrap;
  overflow-x: auto;
  background-color: lightgrey;
}
h2 {
  margin-left: 10px;
  padding-top: 5px;
}
ul {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  width: 100%;
  li {
    width: calc(100% / 4 - 10px);
    display: inherit;
  }
}
</style>
