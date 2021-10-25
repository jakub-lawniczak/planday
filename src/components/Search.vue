<template>
  <form class="search" method="GET" action="/">
    <input
      class="search__input"
      placeholder="Search picture"
      name="search"
      :value="search"
      type="search"
    />
    <button class="search__submit" type="submit">
      <img src="@/assets/loupe.svg" alt="loupe" class="search__loupe" />
    </button>
  </form>
</template>
<script>
export default {
  props: {
    search: {
      type: String,
      default: "",
    },
  },
};
</script>
<style lang="scss" scoped>
.search {
  display: block;
  width: 320px;
  height: 42px;
  margin: 20px auto;
  position: relative;

  &__input {
    width: 100%;
    height: 100%;
    font-size: 16px;
    border: 1px solid #189bd6;
    color: #787878;
    border-radius: 4px;
    padding: 10px;
    &:focus {
      border-width: 2px;
      outline: 0;
    }
  }
  &__submit {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    width: 50px;
    background-color: transparent;
    border: 0;
    cursor: pointer;
  }
}
</style>
