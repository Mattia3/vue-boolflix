<template>
  <div class="col p-0 my-col">
    <div class="card">
      <div class="flip-card-front">
        <img class="my-img" :src="imgPath(movie.poster_path)" alt="" />
      </div>
      <div class="my-card-text">
        <span class="my-2">{{ movie.title || movie.name }}</span>

        <br />
        <div
          class="my-2"
          v-if="
            movie.original_title !== movie.title ||
            movie.original_name !== movie.name
          "
        >
          {{ movie.original_title || movie.original_name }}
        </div>

        <img
          class="bandiere-immagini"
          :src="
            !langFlags[movie.original_language]
              ? urlWord
              : langFlags[movie.original_language]
          "
          alt=""
        />
        <br />

        <i
          v-for="icon in 5"
          :key="icon"
          :class="
            icon <= getNumberoIntero(movie) ? 'fa fa-star' : 'fa fa-star-o '
          "
          aria-hidden="true"
        ></i>
        <br />
        <div class="pt-3" v-if="movie.overview ? 'd-none' : ''">TRAMA</div>
        <br />
        {{ movie.overview }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {
      langFlags: {
        it: "https://upload.wikimedia.org/wikipedia/commons/c/ca/Bandiera_italiana_foto.svg",
        en: "https://www.novalibandiere.it/wp-content/uploads/Gran-bretagna.jpg",
        de: "https://upload.wikimedia.org/wikipedia/commons/thumb/b/ba/Flag_of_Germany.svg/1920px-Flag_of_Germany.svg.png",
        es: "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Flag_of_Spain.svg/1280px-Flag_of_Spain.svg.png",
        usa: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e2/Flag_of_the_United_States_%28Pantone%29.svg/1920px-Flag_of_the_United_States_%28Pantone%29.svg.png",
      },
      urlWord:
        "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Earth_Eastern_Hemisphere.jpg/260px-Earth_Eastern_Hemisphere.jpg",
    };
  },
  props: {
    movie: Object,
  },

  methods: {
    imgPath(posterPath) {
      const pathUrl = "https://image.tmdb.org/t/p/";
      const imgSize = "w342";

      if (!posterPath) {
        return require("@/assets/Site-logo.webp");
      }
      return pathUrl + imgSize + posterPath;
    },

    getNumberoIntero(type) {
      let votoFinale = type.vote_average / 2;
      return Math.ceil(votoFinale);
    },
  },
};
</script>

<style lang="scss">
.my-img {
  width: 100%;
  height: 100%;
  padding: 0 10px;
}

.my-col {
  position: relative;
  perspective: 1000px;
}

.my-col:hover .card {
  transform: rotateY(180deg);
}

.flip-card-front,
.my-card-text {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  backface-visibility: hidden;
  height: 100%;
}
.my-card-text {
  transform: rotateY(180deg);
  background-color: black;
  color: white;
  height: 100%;
  padding: 20px 20px;
  text-align: center;
}

.col .card {
  transition: transform 0.6s;
  transform-style: preserve-3d;
  height: 600px;
  background-color: transparent;
  margin-bottom: 55px;
  border: none;
  position: relative;
}
</style>
