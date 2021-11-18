<template>
  <div id="app" class="">
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

    <div class="background-color">
      <div class="row row-cols-3 container m-auto py-5">
       <div class="col"  v-for="movie in movies" :key="movie.id">
          <ul>
            <li>
             <img :src="imgPath(movie.poster_path)" alt="">
              Title: {{ movie.title }} <br> 
              Title Original: {{ movie.original_title }} <br>
              Nazionalità: <img class="bandiere-immagini" :src="!langFlags[movie.original_language] ? urlWord : langFlags[movie.original_language]" alt=""> <br>
              Voto: <i v-for="icon in 5" :key="icon" :class="icon <= getNumberoIntero(movie) ? 'fa fa-star' :  'fa fa-star-o '" aria-hidden="true"></i>
                 
            </li>
          </ul>
        </div>
      </div>

     <h1>Serie tv</h1>
      <div class="row row-cols-3 container m-auto mt-5">
        
        <div class="col" v-for="serie in series" :key="serie.id">
          <ul>
            <li>
              <img :src="imgPath(serie.poster_path)" alt="">
              Title: {{serie.name}} <br> 
              Title Original: {{serie.original_name}} <br>     
              Nazionalità: <img class="bandiere-immagini" :src="!langFlags[serie.original_language] ? urlWord : langFlags[serie.original_language]" alt=""> <br>
              Voto: <i v-for="icon in 5" :key="icon" :class="icon <= getNumberoIntero(serie) ? 'fa fa-star' :  'fa fa-star-o '" aria-hidden="true"></i>
            </li>
          </ul>
        </div>
      </div>
    </div>
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
      urlWord: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Earth_Eastern_Hemisphere.jpg/260px-Earth_Eastern_Hemisphere.jpg",
      
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
    },

    imgPath(posterPath){
     const pathUrl = "https://image.tmdb.org/t/p/";
     const imgSize = "w342";
     
      if(!posterPath){
        return require("@/assets/logo.png")
      }
      return pathUrl + imgSize + posterPath;
    },

    getNumberoIntero(type){
      let votoFinale = type.vote_average / 2;
      return Math.ceil( votoFinale ) 
    },

   


   
  },

 
}
  
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
@import "~font-awesome/css/font-awesome.min.css";

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

ul{
  list-style: none;
}

.background-color{
  background-color: lightgray;
}
</style>
