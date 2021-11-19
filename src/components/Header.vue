<template>
  <header>
    <div class="header-container">
      <h1 class="text-danger">BOOLFlIX</h1>
      <div class="my-imput-group">
        <input
          type="text"
          placeholder="Cerca un Film.."
          v-model="inputText"
          @keyup.enter="addMovie()"
        />
        <div class="input-group-append">
          <button class="btn btn-danger" @click="addMovie()" type="button">
            Cerca
          </button>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
import axios from "axios";
export default {
  name: "Header",
  data() {
    return {
      apiKey: "66da9c9715a8aa6ea7123977e1274068",
      apiUrl: "https://api.themoviedb.org/3",
      inputText: "",
      language: "",
      movies: [],
      series: [],
    };
  },
  methods: {
    searchAll(url, textToSearch, dataKey) {
      axios
        .get(this.apiUrl + url, {
          params: {
            api_key: this.apiKey,
            query: textToSearch,
          },
        })
        .then((resp) => {
          this[dataKey] = resp.data.results;
          this.$emit("getData", this.movies, this.series);
        });
    },
    addMovie() {
      this.searchAll("/search/movie", this.inputText, "movies");
      this.searchAll("/search/tv", this.inputText, "series");
    },
  },
};
</script>

<style lang="scss"></style>
