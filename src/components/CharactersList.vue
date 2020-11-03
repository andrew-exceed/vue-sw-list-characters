<template>
  <div class="hello">
    <ul>
        <li v-for='(char, index) in charactersList' v-bind:key='index' @click='showModal(char.url)'>
            <img :src="`/img/${char.name.split(' ').join('')}.jpg`" />
            <p>{{char.name}}</p>
        </li>
    </ul>
    <div class="pagination">
        <div class="prev" @click='prevPage'>
            <a v-if='this.prevPageValue' @click='prevPage'>&lt;prev</a>
        </div>
        <div v-for="(q, index) in allPageCount" :key="index">
            <a v-if="this.currentPage != (index+1)" @click='toPage(index + 1)'>{{q}}</a>
            <div v-else>{{q}}</div>
        </div>
        <div  class="next">
            <a v-if='this.nextPageValue'  @click='nextPage'>next></a>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'CharactersList',
    data(){
        return{
            charactersList: Array,
            nextPageValue: null,
            prevPageValue: null,
            currentPage: Number,
            allPageCount: Number,
        }
    },
    mounted() {
        fetch('https://swapi.dev/api/people/')
        .then((response) => {
            return response.json();
        })
        .then((data) => {
            this.updateList(data);
            this.allPageCount = Math.ceil(data.count / data.results.length)
            console.log("123123123", this.allPageCount)
        });
    },
    methods:{   
        // getImgUrl(q) {
        //     return require(`@/assets/${q.toString().split(' ').join('')}.jpg`)
        // },
        updateList(data){
            console.log('update list', data);
            this.charactersList = data.results;
            this.nextPageValue = data.next;
            this.prevPageValue = data.previous;
            this.getCurrentPage();
            
        },
        nextPage(){
            fetch(this.nextPageValue)
            .then((response) => {
                return response.json();
            })
            .then((data) => {
                this.updateList(data);
            }); 
        },
        prevPage(){
            fetch(this.prevPageValue)
            .then((response) => {
                return response.json();
            })
            .then((data) => {
                this.updateList(data);
            }); 
        },
        toPage(newUrl){
            console.log("ToPage", newUrl);   
            fetch(`https://swapi.dev/api/people/?page=${newUrl}`)
            .then((response) => {
                return response.json();
            })
            .then((data) => {
                this.updateList(data);
            }); 
        },
        getCurrentPage(){
            if(this.nextPageValue !== null){
                this.currentPage = +this.nextPageValue.substr(-1)-1;
                console.log('next Page', this.currentPage+1);
            }else{
                this.currentPage = this.allPageCount;
                console.log('ELSE',this.currentPage, this.allPageCount )

            }
        },
        showModal(url){
            this.$emit('show-modal', url);
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
    justify-content: space-between;
    padding: 0;
}
li {
  display: block;
  width: 150px;
  /* height: 150px; */
  background-color: #42b983;
  margin: 5px 10px;
  cursor: pointer;  
  padding: 5px;
  box-sizing: border-box;
}
img{
    width: 100px;
}
a {
  color: #42b983;
  cursor: pointer;
}
.pagination{
    display: flex;
    justify-content: space-around;
}
.next, .prev{
    cursor: pointer;
    width: 50px;
}
</style>
