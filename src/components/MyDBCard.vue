<template>
  <div class="total">
    <h2>Film</h2>
    <div v-if="desiredMovieCards" class="film">
      <div class="item_card">
        <img
          class="poster"
          :src="posterRoot + desiredMovieCards.poster_path"
          alt=""
        />
        <div class="titolo">Titolo: {{ desiredMovieCards.title }}</div>
        <div class="titolo_originale">
          Titolo originale: {{ desiredMovieCards.original_title }}
        </div>
        <div id="lingua">
          Lingua originale:
          <img
            :src="flagRoot + fixFlag(desiredMovieCards.original_language)"
            alt="Bandiera flag"
          />
        </div>
        <div class="voto">Voto: {{ desiredMovieCards.vote_average }}</div>
      </div>
    </div>

    <div v-if="desiredSeriesCards" class="serie">
      <h2>Serie TV</h2>
      <div class="item_card">
        <div class="titolo">Titolo: {{ desiredSeriesCards.name }}</div>
        <div class="titolo_originale">
          Titolo originale: {{ desiredSeriesCards.original_name }}
        </div>
        <div id="lingua">
          Lingua originale:
          <img
            :src="flagRoot + fixFlag(desiredSeriesCards.original_language)"
            alt="Bandiera flag"
          />
        </div>
        <div class="voto">Voto: {{ desiredSeriesCards.vote_average }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyDBCard',
  data() {
    return {
      flagRoot: `https://countryflagsapi.com/svg/`,
      posterRoot: 'https://image.tmdb.org/t/p/w185',
    };
  },
  props: {
    desiredMovieCards: Object,
    desiredSeriesCards: Object,
  },
  methods: {
    fixFlag(flag) {
      if (flag == 'en') {
        return (flag = 'us');
      } else if (flag == 'ja') {
        return (flag = 'jp');
      } else if (flag == 'hi') {
        return (flag = 'in');
      } else if (flag == 'cs') {
        return (flag = 'cz');
      } else if (flag == 'ko') {
        return (flag = 'kr');
      } else if (flag == 'sv') {
        return (flag = 'ch');
      }
      return flag;
    },
    /*  getPoster(posterEnd) {
      this.posterEnd = desiredMovieCards.poster_path;
      return posterEnd;
      console.log('poster', this.posterEnd);
    }, */
  },
};
</script>

<style lang="scss" scoped>
.item_card {
  background: lightgreen;
  margin: 10px;
  #lingua {
    img {
      width: 30px;
      display: inline-block;
    }
  }
}
.poster {
  width: 185px;
}
h2 {
  margin-left: 10px;
}
</style>
