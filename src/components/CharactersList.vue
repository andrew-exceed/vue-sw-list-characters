<template>
  <div class="hello">
    <ul>
        <li v-for='(char, index) in charactersList' v-bind:key='index'>
        {{char.name}}
        </li>
    </ul>
    <div class="pagination">
        <div v-if='this.prevPageValue != null' class="prev" @click='prevPage'>prev</div>
        <div v-if='this.nextPageValue != null' class="next" @click='nextPage'>next</div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'CharactersList',
    data(){
        return{
            charactersList:Array,
            nextPageValue: null,
            prevPageValue: null,
        }
    },
    mounted() {
        fetch('https://swapi.dev/api/people/')
        .then((response) => {
            return response.json();
        })
        .then((data) => {
            console.log(data);
            this.charactersList = data.results;
            this.nextPageValue = data.next;
            this.prevPageValue = data.previous;
        });
    },
    methods:{
        nextPage(){
           fetch(this.nextPageValue)
            .then((response) => {
                return response.json();
            })
            .then((data) => {
                this.charactersList = data.results;
                this.nextPageValue = data.next;
                this.prevPageValue = data.previous;
            }); 
        },
        prevPage(){
           fetch(this.prevPageValue)
            .then((response) => {
                return response.json();
            })
            .then((data) => {
                this.charactersList = data.results;
                this.nextPageValue = data.next;
                this.prevPageValue = data.previous;
            }); 
        },
    },
}
</script>

<style scoped>
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
.pagination{
    display: flex;
    justify-content: space-around;
}
.next, .prev{
    cursor: pointer;
}
</style>
