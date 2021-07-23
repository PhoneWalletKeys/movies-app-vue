<template>
  <div class="home">
    <h2>Add a movie</h2>
    <button v-on:click="createMovie()">Add that Movie</button>
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" :key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
      <h3>Plot: {{ movie.plot }}</h3>
    </div>
  </div>
</template>
<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Give this a watch.",
      movies: [],
      title: "Title",
      year: 1991,
      plot: "Plot",
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies:function () {
    axios.get("http:localhost:3000/movies").then((response) => {
        this.movies = response.data;
        console.log("All Movies:", this.movies);
    })
  },
  createMovie: function () {
      console.log("added the movie");
      var params = {
        title: "Point Break",
        year: 1991,
        plot: "Johnny Utah tries to stop a gang of bank robbers.",
        director: "Kathryn Bigelow",
      };
      axios
        .post("http://localhost:3000/movies", params)
        .then((response) => {
          console.log("Success!", response.data);
          this.movies.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
