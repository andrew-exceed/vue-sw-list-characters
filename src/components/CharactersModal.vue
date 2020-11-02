<template>

    <template >
    <div class="overlay">
    </div>
    <div class="modal">
        <p>{{character.name}}</p>
        <p>{{character.birth_year}}</p>
        <p>{{character.hair_color}}</p>
        <p>{{character.height}}</p>
    </div>
    </template>

</template>

<script>
export default {
    name: 'CharactersModal',
    props:['characterUrl'],
    data(){
        return{
            character: 1,
        }
    },
     mounted() {
         console.log('char', this.characterUrl)
        fetch(this.characterUrl)
        .then((response) => {
            return response.json();
        })
        .then((data) => {
            console.log('char',data);
            this.character = data;
        });
    },
}
</script>

<style scoped>
.overlay{
    width: 100%;
    height: 100vh;
    background: grey;
    opacity: 0.8;
    position: absolute;
    top: 0;
    left: 0;
}
.modal{
    width: 100%;
    max-width: 500px;
    position: relative;
    margin: 0 auto;
    height: 300px;
    background:coral;
    border-radius: 10px;
    top: -200px;
    display: flex;
    flex-direction: column;
}
h3 {
  margin: 40px 0 0;
}
ul {
  display: flex;
  flex-wrap: wrap;
}
li {
  display: block;
  width: 100px;
  height: 100px;
  background-color: #42b983;
  margin: 5px 10px;
}
a {
  color: #42b983;
}
</style>
