<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>Title: <input type="text" v-model="newMovieParams.title" /></div>
    <div>Plot: <input type="text" v-model="newMovieParams.plot" /></div>
    <div>Year: <input type="text" v-model="newMovieParams.year" /></div>
    <button v-on:click="createMovie()">New Movie</button>
    <h1>Movies</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <p>Title: {{ movie.title }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <p>Year: {{ movie.year }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Movies",
      movies: [],
      newMovieParams: {},
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      axios
        .post("http://localhost:3000/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.movies.push(response.data);
        });
    },
  },
};
</script>
