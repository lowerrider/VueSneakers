<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      :price="12999"
      title="Мужские Кроссовки Nike Blazer Mid Suede"
      imageUrl="/sneakers/sneakers-1.jpg"
      isAded
      isFavorite
      :onClickAdd="onClickAdd" />
    <Card />
    <Card />
    <Card />
    <Card />
    <Card />
  </div>
</template>

<script setup>
import Card from "./Card.vue";

const onClickAdd = () => {
  alert("add");
};
</script>

<style></style>
