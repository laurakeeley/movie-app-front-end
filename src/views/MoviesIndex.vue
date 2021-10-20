<template>
  <div class="movies-index">
    <h1>All Movies</h1>
    <div class="row">
      <div class="col-sm-6" v-for="movie in movies" v-bind:key="movie.id">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card-text">
              {{ movie.year }} <br />
              {{ movie.plot }}
            </p>
            <router-link
              :to="`/movies/${movie.id}`"
              class="btn btn-outline-info"
              >Movie Deets</router-link
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
  },
};
</script>
