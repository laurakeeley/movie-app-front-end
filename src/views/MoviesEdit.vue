<template>
  <div class="movies-edit">
    <form v-on:submit.prevent="updateMovies()">
      <h1>Edit Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="editMovieParams.title" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="editMovieParams.plot" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="editMovieParams.year" />
      </div>
      <input type="submit" value="Update" />
    </form>

    editMovieParams: {{ editMovieParams }}
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      editMovieParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/movie/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.editMovieParams = response.data;
    });
  },
  methods: {
    updateMovies: function () {
      axios
        .patch(`/movies/${this.editMovieParams.id}`, this.editMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/movies/${response.data.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
