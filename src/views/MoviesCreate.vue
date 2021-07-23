<template>
  <div>
    <h1>Add a Movie</h1>
    <p>Title:</p>
    <input type="text" v-model="title" />
    <p>Year:</p>
    <input type="text" v-model="year" />
    <p>Plot:</p>
    <input type="text" v-model="plot" />
    <p></p>
    <button v-on:click="addMovie">Add Movie</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      title: "Title",
      year: 1900,
      plot: "Plot",
    };
  },
  methods: {
    addMovie: function () {
      console.log("Add movie");
      var params = { title: this.title, year: this.year, plot: this.plot };
      axios
        .post("http://localhost:3000/movies", params)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>