<template>
  <div class="record">
    <div class="record__imgBox">
      <img :src="img" :alt="description" />
    </div>
    <div class="record__text">
      <h2 class="record__title" v-html="title"></h2>
      <p class="record__description" v-html="description"></p>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    img: {
      type: String,
      default: "",
    },
    title: {
      type: String,
      default: "",
    },
    description: {
      type: String,
      default: "",
    },
  },
};
</script>
<style lang="scss" scoped>
.record {
  &__title {
    font-size: 32px;
  }
  &__description {
    font-size: 12px;
    flex-wrap: 300;
  }
  &__imgBox {
    width: 300px;
    height: 450px;
    display: flex;
    align-items: center;
    background-color: rgba(255, 255, 255, 0.15);
    position: relative;
    border-radius: 8px;
    overflow: hidden;
    &:before {
      content: "";
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      background-color: #000;
      border-radius: 8px;
      z-index: -1;
    }
    img {
      max-width: 100%;
    }
  }
}
</style>
