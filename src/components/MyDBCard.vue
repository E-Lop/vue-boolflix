<template>
  <div class="item_card">
    <div class="titolo">Titolo: {{ desiredCards.title }}</div>
    <div class="titolo_originale">
      Titolo originale: {{ desiredCards.original_title }}
    </div>
    <div id="lingua">
      Lingua originale:
      <img
        :src="flagRoot + fixFlag(desiredCards.original_language)"
        alt="Bandiera flag"
      />
    </div>
    <div class="voto">Voto: {{ desiredCards.vote_average }}</div>
  </div>
</template>

<script>
export default {
  name: 'MyDBCard',
  data() {
    return {
      flagRoot: `https://countryflagsapi.com/svg/`,
      // flag: this.desiredCards.original_language,
    };
  },
  props: {
    desiredCards: Object,
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
</style>
