<template>
  <div class="total">
    <!-- parte dedicata ai film -->
    <div v-if="desiredMovieCards" class="film">
      <div
        class="item_card"
        @mouseenter="moreinfo = true"
        @mouseleave="moreinfo = false"
      >
        <div v-if="!moreinfo" class="copertina">
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
            alt="Copertina di ${desiredMovieCards.title}"
          />
        </div>
        <div v-else class="informazioni">
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
            Voto:
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
            <!-- tasto per rendere visibile il cast -->
            <button
              @click.prevent="getTheCast(desiredMovieCards.id)"
              class="moreBtn"
            >
              altro
            </button>
          </div>
          <div class="overview">Overview: {{ desiredMovieCards.overview }}</div>
        </div>
      </div>
    </div>
    <!-- parte dedicata alle serie tv -->
    <div v-if="desiredSeriesCards" class="serie">
      <div
        class="item_card"
        @mouseenter="moreinfo = true"
        @mouseleave="moreinfo = false"
      >
        <div v-if="!moreinfo" class="copertina">
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
        </div>
        <div v-else class="informazioni">
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
              v-for="m in getStars(desiredSeriesCards.vote_average)"
              :key="m"
              class="fa-solid fa-star"
            ></i>
            <i
              v-for="m in 5 - getStars(desiredSeriesCards.vote_average)"
              :key="m"
              class="fa-regular fa-star"
            ></i>
          </div>
          <div class="overview">
            Overview: {{ desiredSeriesCards.overview }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'MyDBCard',
  data() {
    return {
      flagRoot: `https://countryflagsapi.com/svg/`,
      posterRoot: 'https://image.tmdb.org/t/p/w342',
      moreinfo: false,
      showCast: false,
      castArray: [],
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
    getTheCast(pippo) {
      axios
        .get(
          'https://api.themoviedb.org/3/movie/${pippo}/credits?api_key=8c2a59c90f2e8f4d2da84becf8da96e9&language=it-IT'
        )
        .then((response) => {
          const castResult = response.data.cast;
          this.castArray = castResult;
          console.log('cast', this.castArray);
        });
    },
  },
};
</script>

<style lang="scss" scoped>
.item_card {
  background: black;
  margin: 10px;
  display: inline-block;
  height: 514px;
  #lingua {
    img {
      width: 30px;
      display: inline-block;
    }
  }
}
.item_card {
  div {
    overflow-wrap: break-word;
    color: white;
  }
}
.poster {
  width: 342px;
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
.informazioni {
  width: 342px;
  height: 514px;
  padding: 10px;
  font-size: 1.2rem;
  overflow-y: auto;
}
.voto {
  position: relative;
}
.moreBtn {
  position: absolute;
  right: 0;
  top: 0;
}
</style>
