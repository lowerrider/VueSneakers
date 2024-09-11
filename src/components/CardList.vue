<template>
  <div class="grid grid-cols-4 gap-5" v-auto-animate>
    <Card
      v-for="item in items"
      :id="item.id"
      :key="item.id"
      :price="item.price"
      :title="item.title"
      :imageUrl="item.imageUrl"
      :isFavorite="item.isFavorite"
      :onClickAdd="isFavorites ? null : () => emit('addToCart', item)"
      :onClickFavorite="isFavorites ? null : () => emit('addToFavorite', item)"
      :isAded="item.isAdded"
    />
  </div>
</template>

<script setup>
import Card from "./Card.vue";

defineProps({
  items: Array,
  isFavorites: Boolean,
});

const emit = defineEmits(["addToFavorite", "addToCart"]);
// const onClickAdd = () => {
//   emit("addToFavorite", item);
// };
</script>

<style></style>
