<template>
  <div class="header_space">
    <div class="logo">LOGO</div>
    <div class="search_space">
      <input
        type="text"
        id="content_search"
        name="content_search"
        placeholder="Effettua una ricerca"
      />
      <button>Cerca</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyHeader',
};
</script>

<style lang="scss" scoped>
.header_space {
  background-color: lightsalmon;
  display: flex;
  padding: 10px;
}
.logo {
  width: 50%;
}
.search_space {
  width: 50%;
  display: flex;
  justify-content: end;
  align-content: center;
}
</style>
