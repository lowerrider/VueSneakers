<script setup>
import CardList from "./components/CardList.vue";
import Header from "./components/Header.vue";
import Drawer from "./components/Drawer.vue";
import { onMounted, ref, reactive, watch, provide } from "vue";
import axios from "axios";

const items = ref([]);

const filters = reactive({
  sortBy: "title",
  searchQuery: "",
});

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value;
};

const onChangeSearchInput = (ev) => {
  filters.searchQuery = ev.target.value;
};

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(
      `https://e2439cabf4a282f6.mokky.dev/favorites`
    );
    items.value = items.value.map((item) => {
      const favorite = favorites.find(
        (favorite) => favorite.parentId === item.id
      );

      if (!favorite) {
        return item;
      }
      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id,
      };
    });
  } catch (e) {
    console.log(e);
  }
};

const addToFavorite = async (item) => {
  try {
    if (!item.isFavorite) {
      const obj = {
        parentId: item.id,
      };
      item.isFavorite = true;
      const { data } = await axios.post(
        `https://e2439cabf4a282f6.mokky.dev/favorites`,
        obj
      );

      item.favoriteId = data.id;
      console.log(data);
    } else {
      item.isFavorite = false;

      await axios.delete(
        `https://e2439cabf4a282f6.mokky.dev/favorites/${item.favoriteId}`
      );
      item.favoriteId = null;
    }
  } catch (err) {
    console.log(err);
  }
};

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy,
    };
    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`;
    }
    const { data } = await axios.get(
      `https://e2439cabf4a282f6.mokky.dev/items`,
      { params }
    );
    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      isAded: false,
      favoriteId: null,
    }));
  } catch (e) {
    console.log(e);
  }
};

onMounted(async () => {
  await fetchItems();
  await fetchFavorites();
});

watch(filters, fetchItems);

provide("addToFavorite", addToFavorite);
</script>

<template>
  <!-- <Drawer /> -->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header />

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>
        <div class="flex gap-4">
          <select
            @change="onChangeSelect"
            class="py-2 px-3 border rounded-md outline-none"
            name=""
            id=""
          >
            <option value="name">По названию</option>
            <option value="price">Дешевые</option>
            <option value="-price">Дорогие</option>
          </select>
          <div class="relative">
            <img class="absolute left-5 top-3" src="/search.svg" alt="" />
            <input
              @input="onChangeSearchInput"
              class="border border-gray-200 rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
              placeholder="Поиск..."
            />
          </div>
        </div>
      </div>
      <div class="mt-10">
        <CardList :items="items" @addToFavorite="addToFavorite" />
      </div>
    </div>
  </div>
</template>

<style scoped></style>

<!-- 3 54 -->
