<template>
  <div id="app">
    <PaginationFilter v-if="activeTab===1" />
    <!-- <div v-for="character in characters" :key="character.id">
      <CharacterCard :character="character" />
    </div> -->
    <CharacterCard v-else v-for="character in characters" :key="character.id" :character="character"/>
  </div>
</template>

<script>
import axios from 'axios';
import CharacterCard from './components/CharacterCard.vue';
import PaginationFilter from './components/PaginationFilter.vue';
const activeTab = 1;
export default {
  components: { CharacterCard, PaginationFilter },
  data() {
    return {
      characters: [],
      activeTab: 1,
    };
  },
  created() {
     this.fetchCharacters();
  },
  methods: {
    async fetchCharacters() {
      try {
        const response = await axios.get('https://rickandmortyapi.com/api/character');
        this.characters = response.data.results;
      } catch (error) {
        console.error('Ошибка при загрузке персонажей:', error);
      }
    }
  },
};
</script>