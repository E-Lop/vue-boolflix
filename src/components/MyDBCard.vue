<template>
  <div class="total">
    <!-- PARTE DEDICATA AI FILM -->
    <div v-if="desiredMovieCards" class="film">
      <div
        class="item_card"
        @mouseenter="moreinfo = true"
        @mouseleave="moreinfo = false"
      >
        <!-- senza mouseover di default visualizza le locandine -->
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
            :src="require('../assets/img/no_picture_342x514.png')"
            alt="Copertina di ${desiredMovieCards.title}"
          />
        </div>
        <!-- al mouseover visualizza le informazioni del film -->
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
          <div v-if="showCast" class="castGeneri">
            <ul>
              <li v-for="(actor, index) in castArray" :key="index">
                Interprete: {{ actor.original_name }}
              </li>
            </ul>
          </div>
          <div class="overview">Trama: {{ desiredMovieCards.overview }}</div>
        </div>
      </div>
    </div>

    <!-- PARTE DEDICATA ALLE SERIE TV -->

    <div v-if="desiredSeriesCards" class="serie">
      <div
        class="item_card"
        @mouseenter="moreinfo = true"
        @mouseleave="moreinfo = false"
      >
        <!-- al mouseover visualizza le informazioni del film -->
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
        <!-- al mouseover visualizza le informazioni della serie tv -->
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
            <!-- tasto per rendere visibile il cast -->
            <button
              @click.prevent="getTheCast(desiredSeriesCards.id)"
              class="moreBtn"
            >
              altro
            </button>
          </div>
          <div v-if="showCast" class="castGeneri">
            <ul>
              <li v-for="(actor, index) in castArray" :key="index">
                Interprete: {{ actor.original_name }}
              </li>
            </ul>
          </div>
          <div class="overview">Trama: {{ desiredSeriesCards.overview }}</div>
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
      // castArray limitato a 5 elementi dallo splice in getTheCast
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
          `https://api.themoviedb.org/3/movie/${pippo}/credits?api_key=8c2a59c90f2e8f4d2da84becf8da96e9&language=it-IT`
        )
        .then((response) => {
          const castResult = response.data.cast;
          // lo slice prende solo i primi 5 risultati dalla risposta API
          this.castArray = castResult.slice(0, 5);
          this.showCast = !this.showCast;
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
