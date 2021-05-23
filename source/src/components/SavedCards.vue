<template>
  <div class="saved-cards" v-if="cards">
    <div
      class="card"
      v-for="(number, index) in cards"
      :key="index"
      @click="handleSelect(number)"
    >
      <input type="radio" name="saved" :checked="selected === number" />
      <div class="card__title">
        {{ number }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SavedCards",
  data: () => ({
    selected: null,
  }),
  props: {
    cards: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    handleSelect(number) {
      this.selected = number;
      this.$emit("select", number);
    },
  },
};
</script>

<style lang="scss" scoped>
.card {
  display: flex;
  cursor: pointer;
  &__title {
    margin-left: var(--indent-sm);
    margin-bottom: var(--indent-xs);
    font-weight: bold;
  }
}
</style>
