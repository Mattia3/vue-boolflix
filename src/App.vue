<template>
  <div id="app">
    <header>
      <div class="header-container">
        <h1 class="text-danger">BOOLFlIX</h1>
        <div class="my-imput-group">
          <input type="text" placeholder="Cerca un Film.." v-model="inputText" @keyup.enter="addMovie">
          <div class="input-group-append">
            <button class="btn btn-primary" type="button" @click="addMovie">Button</button>
          </div>
        </div>
      </div>
    </header>

      <ul>
        <li v-for="movie in movies" :key="movie.id">
          {{ movie.title }} {{ movie.original_title }} <br>
          <img class="bandiere-immagini" :src="langFlags[movie.original_language]" alt=""> {{movie.vote_average}}
        
        </li>
      </ul>

       
      <ul>
        
        <li v-for="serie in series" :key="serie.id">
           {{serie.name}} {{serie.original_name}} <br>     
          <img class="bandiere-immagini" :src="langFlags[serie.original_language]" alt="">
           {{ serie.vote_average }}
        </li>
      </ul>
   
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: 'App',
  data(){
    return{
      apiKey: "66da9c9715a8aa6ea7123977e1274068",
      apiUrl: "https://api.themoviedb.org/3",
      movies: [],
      language: "",
      inputText: "",
      langFlags:{
        it: "https://upload.wikimedia.org/wikipedia/commons/c/ca/Bandiera_italiana_foto.svg",
        en: "https://www.novalibandiere.it/wp-content/uploads/Gran-bretagna.jpg",
        de: "https://upload.wikimedia.org/wikipedia/commons/thumb/b/ba/Flag_of_Germany.svg/1920px-Flag_of_Germany.svg.png",
        es: "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Flag_of_Spain.svg/1280px-Flag_of_Spain.svg.png",
        usa: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e2/Flag_of_the_United_States_%28Pantone%29.svg/1920px-Flag_of_the_United_States_%28Pantone%29.svg.png"
      },
      series: [],
      urlImage: "http://image.tmdb.org/t/p/w500"
    }
  },
  components: {
   
  },
  methods:{
    searchAll(url, textToSearch, dataKey){
      axios.get(this.apiUrl + url, {
        params: {
          api_key: this.apiKey,
          query: textToSearch,
        }
      })
      .then((resp) => {
        this[dataKey] = resp.data.results;
      })
    },

    addMovie(){
      this.searchAll("/search/movie", this.inputText, "movies");
      this.searchAll("/search/tv", this.inputText, "series");
    }
  },

  mounted() {
    
  }
}
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";


.header-container{
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: black;
    height: 80px;
    padding: 10px 20px;
  
    .my-imput-group{
      display: flex;
    }
    
  }

.bandiere-immagini{
  width: 30px;
}
</style>
