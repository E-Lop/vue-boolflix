<template>
  <div>
    <ul>
      <li>
        <MyDBCard
          v-for="(element, index) in receivedResults"
          :key="index"
          :desiredCards="receivedResults[index]"
        />
      </li>
    </ul>
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
