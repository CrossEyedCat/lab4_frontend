<template>
  <div>
    <h2>Избранные элементы пользователя</h2>
    <label for="userId">Введите идентификатор пользователя:</label>
    <input type="text" v-model="userId" id="userId" />
    <button @click="getFavorites">Получить избранные элементы</button>

    <div v-if="favorites.length > 0">
      <h3>Избранные элементы пользователя:</h3>
      <ul>
        <li v-for="item in favorites" :key="item.id">{{ item.name }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      userId: "",
      favorites: [],
    };
  },
  methods: {
    async getFavorites() {
      try {
        const response = await axios.get(
            `http://localhost:10234/get_favorites?userId=${this.userId}`
        );
        this.favorites = response.data;
      } catch (error) {
        console.error("Ошибка при получении избранных элементов:", error);
      }
    },
  },
};
</script>

<style scoped>
/* Здесь можно добавить стили компонента */
</style>