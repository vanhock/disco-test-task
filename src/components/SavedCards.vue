<template>
  <div class="saved-cards">
    <div
      class="card"
      v-for="(card, index) in cards"
      :key="index"
      @click="handleSelect(card)"
    >
      <input type="radio" name="saved" :checked="selected === card?.number" />
      <span class="card__title">
        {{ card.type }} <b>{{ card.number }}</b>
      </span>
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
    handleSelect(card) {
      this.$emit("select", card.number);
    },
  },
};
</script>

<style scoped></style>
