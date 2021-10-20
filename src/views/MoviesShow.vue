<template>
  <div class="movies-show">
    <h1>Movie Deets</h1>
    <h2>{{ movie.title }}</h2>
    <h3>{{ movie.year }}</h3>
    <p>{{ movie.plot }}</p>
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {},
};
</script>
