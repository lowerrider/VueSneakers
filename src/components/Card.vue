<template>
  <div
    class="relative bg-white border border-slate-100 rounded-3xl p-5 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition flex flex-col justify-between"
  >
    <img
      v-if="onClickFavorite"
      @click="onClickFavorite"
      class="absolute top-8 left-8"
      :src="!isFavorite ? '/VueSneakers/like-1.svg' : '/VueSneakers/like-2.svg'"
      alt="like 2"
    />
    <img :src="imageUrl" alt="sneaker" />
    <div class="mt-4">
      <p class="mt-2">{{ title }}</p>

      <div class="flex justify-between mt-5">
        <div class="flex flex-col">
          <span class="text-slate-400">Цена:</span>
          <b>{{ price }} руб.</b>
        </div>
        <img
          v-if="onClickAdd"
          @click="onClickAdd"
          :src="!isAded ? '/VueSneakers/plus.svg' : '/VueSneakers/checked.svg'"
          alt="Plus"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  price: Number,
  isFavorite: Boolean,
  isAded: Boolean,
  onClickAdd: Function,
  onClickFavorite: Function,
});
</script>

<style></style>
