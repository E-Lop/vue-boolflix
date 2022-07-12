<template>
  <div class="item_card">
    <div class="titolo">Titolo: {{ desiredCards.title }}</div>
    <div class="titolo_originale">
      Titolo originale: {{ desiredCards.original_title }}
    </div>
    <div class="lingua">
      Lingua originale: {{ desiredCards.original_language }}
    </div>
    <div class="voto">Voto: {{ desiredCards.vote_average }}</div>
  </div>
</template>

<script>
export default {
  name: 'MyDBCard',
  props: {
    desiredCards: Object,
  },
};
</script>

<style lang="scss" scoped>
.item_card {
  background: lightgreen;
  margin: 10px;
}
</style>
