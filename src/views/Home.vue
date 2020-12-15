

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="createPlaces()">mention a new places</button>
    <div v-for="place in places">
      <p><h4>{{place.name}}</h4>
      <p><h4>{{place.address}}</h4>
      <h3>{{ message2 }}</h3>
    <!-- <button v-on:click="indexPlaces()">show the places</button> -->
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      message2: "**************",
      places: [],
    };
  },
  created: function () {
    this.indexPlaces();
  },
  methods: {
    indexPlaces: function () {
      console.log("index of places");
      axios.get("/api/places").then((response) => {
        console.log(response.data);
        this.places = response.data;
      });
    },
    createPlaces: function () {
      console.log("mention new place");
      var params = {
        name: "forest",
        address: "red tree lane",
      };
      axios.post("/api/places", params).then((response) => {
        console.log(response.data);
        this.places = response.data;
      });
    },
  },
};
</script>
