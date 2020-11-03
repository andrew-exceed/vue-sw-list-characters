<template>
<div class="content">
  <h1>Star Wars Characters</h1>
  <CharactersList @show-modal='showModal' />
  <CharactersModal :characterUrl="visibleChar" @close="closeModal" :isModalVisible='isModalVisible'/>
</div>
</template>

<script>
import CharactersList from './components/CharactersList.vue';
import CharactersModal from './components/CharactersModal.vue';

export default {
  name: 'App',
  data(){
    return{
      visibleChar: null,
      isModalVisible: false,
    }
  },
  components: {
    CharactersList,
    CharactersModal,
  },
  methods: {
    showModal(charUrl) {
      this.visibleChar = charUrl;
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    }
  },
}
</script>

<style>
.content{
  max-width: 1000px;
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
