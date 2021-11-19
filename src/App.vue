<template>
  <div id="app">
    <Header @getData="listenData"></Header>

    <div class="background-color">
      <div class="container">
        <div v-if="movies.length > 0">
          <h1 class="title-film">FILM</h1>
          <div class="row row-cols-3 m-auto py-5">
            <Card v-for="movie in movies" :key="movie.id" :movie="movie"></Card>
          </div>
        </div>
        <div v-if="series.length > 0">
          <h1 class="title-film">SERIE TV</h1>
          <div class="row row-cols-3 m-auto mt-5">
            <Card v-for="serie in series" :key="serie.id" :movie="serie"></Card>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import Header from "./components/Header.vue";

export default {
  name: "App",
  components: {
    Card,
    Header,
  },

  data() {
    return {
      movies: "",
      language: "",
      series: "",
    };
  },

  methods: {
    listenData(film, serie) {
      this.movies = film;
      this.series = serie;
      console.log(film);
      console.log(serie);
    },
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
@import "~font-awesome/css/font-awesome.min.css";

.header-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: black;
  height: 80px;
  padding: 10px 20px;

  .my-imput-group {
    display: flex;
  }
}

.bandiere-immagini {
  width: 30px;
}

.background-color {
  background-color: gray;
  height: 100%;
}

.title-film {
  text-align: center;
  font-weight: bold;
  padding-top: 40px;
  color: red;
}
</style>
