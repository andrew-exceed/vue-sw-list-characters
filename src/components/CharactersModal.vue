<template>

    <div v-show="isModalVisible" @click="close" class="overlay">
    </div>
    <div v-show="isModalVisible"  class="modal">
        <p>
            <!-- <img src="https://i1.wp.com/sova.ponominalu.ru/wp-content/uploads/2018/03/filmz.ru_f_88509.jpg?fit=1200%2C794&ssl=1" /> -->
            <!-- <img :src="getImgUrl(character.name)" /> -->
            <img :src="character.name && `/img/${character.name.split(' ').join('')}.jpg`" />
        </p>
        <p>{{character.name}}</p>
        <p>год рождения - {{character.birth_year}}</p>
        <p>цвет волос - {{character.hair_color}}</p>
        <p>рост - {{character.height}}</p>
        <a @click="close" >close</a>
    </div>
</template>

<script>
export default {
    name: 'CharactersModal',
    props:['characterUrl', 'isModalVisible'],
    emits: ["close"],
    data(){
        return{
            character: {},
        }
    },
    
    methods:{
        close(){
            this.$emit('close');
        },
        //  getImgUrl(q) {
        //     if(this.character.name){return require(`@/assets/${q.toString().split(' ').join('')}.jpg`)}
        //     else{return '@/assets/plugImg.jpg'}
        // },
    },
    watch: {
        characterUrl: {
            immediate: true, 
            handler (newUrl, oldUrl) {
                console.log('change new:',newUrl,'old:', oldUrl)
                if(newUrl){
                    fetch(newUrl)
                    .then((response) => {
                        return response.json();
                    })
                    .then((data) => {
                        console.log('char',data);
                        this.character = data;
                    });
                }
            }
        }
    },

}
</script>

<style scoped>
.overlay{
    width: 100%;
    height: 100vh;
    background: rgba(123,123,123,.6);
    position: absolute;
    top: 0;
    left: 0;
}
.modal{
    top: -300px;
    width: 100%;
    max-width: 500px;
    position: relative;
    margin: 0 auto;
    background:blanchedalmond;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    padding-bottom: 10px;
    
}
h3 {
  margin: 40px 0 0;
}
ul {
  display: flex;
  flex-wrap: wrap;
}
img{
    width: 200px;
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
  cursor: pointer;
}
</style>
