<template>
  <div class="pagination-filter">
    <input type="text" v-model="nameFilter" placeholder="Фильтр по имени">
    <select v-model="statusFilter">
      <option value="">Все статусы</option>
      <option value="Alive">Жив</option>
      <option value="Dead">Мертв</option>
      <option value="unknown">Неизвестно</option>
    </select>
   
    
    </div>
    <button type="button" @click="applyName">Поиск</button>
    <button @click="applyFilters">Применить</button>
    <button @click="clearFilters">Сбросить</button>
    <button @click="prevPage" :disabled="currentPage === 1">Предыдущая</button>
    <span>{{ currentPage }}</span>
    <button @click="nextPage" :disabled="currentPage === totalPages">Следующая</button>

    <div v-if="applyNames.length > 0">
    <ul>
      <CharacterCard v-for="character in applyNames" :key="character.id" :character="character"/>
      <li v-for="character in applyNames" :key = "character.id">
      {{ character.name }}
     
    </li>
    </ul>


    <!-- <input type="text" v-model="nameFilter" placeholder="Введите имя персонажа">
    <button type="button" @click="applyName">Поиск</button>

    
    <div v-if="applyNames.length > 0">
      <ul>
        <li v-for="character in applyNames" :key="character.id">
          {{ character.name }}
        </li>
      </ul>
    </div>

    <div v-else>
      <p>Нет персонажей с таким именем.</p>
    </div> -->

  </div>
</template>

<script>
import CharacterCard from './CharacterCard.vue';
import axios from 'axios';
export default {
  components:{
    CharacterCard
  },
  data() {
    return {
      nameFilter: '',
      statusFilter: '',
      applyNames:[],
      currentPage: 1,
      totalPages: 1,
      characters: []
      
    };
  },
  created() {
     this.fetchCharacters();
  },
  
  methods: {
    async applyName() {
      // Здесь вы можете использовать ваш API и выполнить запрос для фильтрации персонажей по имени
      try {
        const response = await fetch(`https://rickandmortyapi.com/api/character/?name=${this.nameFilter}&status=${this.statusFilter}`);
        const data = await response.json();
        this.applyNames = data.results;
      } catch (error) {
        console.error('Ошибка при загрузке данных:', error);
      }
    },
    async fetchCharacters() {
      try {
        const response = await axios.get('https://rickandmortyapi.com/api/character');
        this.characters = response.data.results;
      } catch (error) {
        console.error('Ошибка при загрузке персонажей:', error);
      }
    }
  }
};
</script>

<style scoped>
.pagination-filter {
  margin-bottom: 20px;
}
</style>