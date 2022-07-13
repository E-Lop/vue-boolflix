<template>
  <div>
    <div class="film">
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
    <div class="serie">
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
  methods: {
    showFilteredContent() {
      console.log('array', arguments);
    },
  },
};
</script>

<style lang="scss" scoped></style>
