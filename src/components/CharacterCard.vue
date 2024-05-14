<template>
  <div class="character-card">
  
    <img class="avatar" :src="`https://rickandmortyapi.com/api/character/avatar/${character.id}.jpeg`" alt="">
    <h2>{{ character.name }}</h2>
    <p>Status: {{ character.status }}</p>
    <p>Species: {{ character.species }}</p>
    <p>Gender: {{ character.gender }}</p>
  </div>
</template>

<script>
export default {
  props: {
    character: Object,
    characterData: Object // Принимаем объект с информацией о персонаже
  },
  methods: {
    
  }
}
</script>

<style scoped>
.character-card {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 10px;
} 
.avatar{
  border-radius: 50%;
}
</style>