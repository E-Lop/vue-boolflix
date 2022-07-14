<template>
  <div class="total">
    <!-- parte dedicata ai film -->
    <div v-if="desiredMovieCards" class="film">
      <div class="item_card">
        <img
          v-if="desiredMovieCards.poster_path"
          class="poster"
          :src="posterRoot + desiredMovieCards.poster_path"
          alt=""
        />
        <!-- fallback per risultati senza immagini -->
        <img
          v-else
          class="poster"
          :src="require('../assets/img/no_picture_185x278.png')"
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
        <div class="voto">
          <i
            v-for="n in getStars(desiredMovieCards.vote_average)"
            :key="n"
            class="fa-solid fa-star"
          ></i>
          <i
            v-for="n in 5 - getStars(desiredMovieCards.vote_average)"
            :key="n"
            class="fa-regular fa-star"
          ></i>
        </div>
      </div>
    </div>
    <!-- parte dedicata alle serie tv -->
    <div v-if="desiredSeriesCards" class="serie">
      <div class="item_card">
        <img
          v-if="desiredSeriesCards.poster_path"
          class="poster"
          :src="posterRoot + desiredSeriesCards.poster_path"
          alt=""
        />
        <!-- fallback per risultati senza immagini -->
        <img
          v-else
          class="poster"
          :src="require('../assets/img/no_picture_185x278.png')"
          alt=""
        />
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
        <div class="voto">
          Voto:
          <i
            v-for="n in getStars(desiredSeriesCards.vote_average)"
            :key="n"
            class="fa-solid fa-star"
          ></i>
          <i
            v-for="n in 5 - getStars(desiredSeriesCards.vote_average)"
            :key="n"
            class="fa-regular fa-star"
          ></i>
        </div>
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
    getStars(api_vote) {
      return Math.round(api_vote / 2);
    },
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
.voto {
  i {
    color: gold;
    font-size: 1.2rem;
  }
}
</style>
