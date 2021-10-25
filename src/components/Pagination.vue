<template>
  <div class="pagination">
    <button
      class="pagination__btn pagination__btn--prev"
      :disabled="ifFirstPage"
      @click="$emit('input', value - 1)"
    >
      <img src="../assets/right-chevron.svg" alt="chevron" />
    </button>
    <p>Page {{ value + 1 }} of {{ numberOfPages }}</p>
    <button
      class="pagination__btn pagination__btn--next"
      :disabled="ifLastPage"
      @click="$emit('input', value + 1)"
    >
      <img src="../assets/right-chevron.svg" alt="chevron" />
    </button>
  </div>
</template>
<script>
export default {
  props: {
    value: {
      type: Number,
      required: true,
    },
    numberOfPages: {
      type: Number,
      required: true,
    },
  },
  computed: {
    ifFirstPage() {
      return this.value === 0;
    },
    ifLastPage() {
      return this.value + 1 === this.numberOfPages;
    },
  },
};
</script>
<style lang="scss" scoped>
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  margin-top: 10px;
  margin-bottom: 30px;

  &__btn {
    display: flex;
    align-items: center;
    justify-content: center;
    border: none;
    border-radius: 5px;
    background-color: #189bd6;
    width: 40px;
    height: 40px;
    margin: 0 10px;
    cursor: pointer;
    &--prev {
      transform: rotateY(180deg);
    }
    &:disabled {
      background: darken(#189bd6, 20%);
    }
    img {
      height: 20px;
    }
  }
}
</style>
