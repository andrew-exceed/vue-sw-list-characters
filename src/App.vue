<template>
<div class="content">
  <h1>Characters</h1>
  <CharactersList  />
  <CharactersModal :characterUrl="activeChar"/>
</div>
</template>

<script>
import CharactersList from './components/CharactersList.vue';
import CharactersModal from './components/CharactersModal.vue';

export default {
  name: 'App',
  data(){
    return{
      activeChar: 'https://swapi.dev/api/people/1/'
    }
  },
  components: {
    CharactersList,
    CharactersModal,
  }
}
</script>

<style>
.content{
  max-width: 1100px;
  width: 100%;
  margin: 0 auto;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
