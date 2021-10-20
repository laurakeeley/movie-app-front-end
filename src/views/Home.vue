<template>
  <div class="home">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="newMovieParams.plot" />
      </div>
      newMovieParams : {{ newMovieParams }}
      <br />
      <input type="submit" value="Create" />
    </form>

    <div class="row">
      <div class="col-sm-6" v-for="movie in movies" v-bind:key="movie.id">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card-text">
              {{ movie.year }} <br />
              {{ movie.plot }}
            </p>
            <router-link :to="`/movies/${movie.id}`" class="btn btn-primary"
              >Movie Deets</router-link
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
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
