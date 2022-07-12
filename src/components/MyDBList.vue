<template>
  <div>
    <ul>
      <li v-for="(element, index) in receivedResults" :key="index">
        {{ element.title }}
        {{ element.original_title }}
        {{ element.original_language }}
        {{ element.vote_average }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'MyDBList',
  data() {
    return {
      receivedArray: [],
    };
  },
  props: {
    receivedResults: Array,
  },
  methods: {
    showFilteredContent() {
      console.log('array', arguments);
    },
  },
};
</script>

<style lang="scss" scoped></style>
