<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :id="item.id"
      :key="item.id"
      :price="item.price"
      :title="item.title"
      :imageUrl="item.imageUrl"
      :isFavorite="item.isFavorite"
      :onClickFavorite="() => emit('addToFavorite', item)"
    />
  </div>
</template>

<script setup>
import Card from "./Card.vue";

defineProps({
  items: Array,
});

const emit = defineEmits(["addToFavorite"]);
// const onClickAdd = () => {
//   emit("addToFavorite", item);
// };
</script>

<style></style>
