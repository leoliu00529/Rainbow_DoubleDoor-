<template>
  <div id="app">
    <img alt="Rainbow logo" src="./assets/rainbow.jpg">
    <HelloWorld msg="This is a website built for DoubleDoor Technologies Technical Challenge"/>
    <button v-on:click="planet()">Well, show me some planets!</button>
    <p> </p>
    <button v-on:click="species()">Something more Interesting? Some species maybe?</button>
    <p> </p>
    <button v-on:click="people()">May the force be with you! Giveme some people!</button>

    <p>{{ this.swdata }}</p>
    <p>{{ this.swdata1 }}</p>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from "axios";

export default {
  name: 'app',
  data() {
    return {
      swdata: "",
      swdata1: "",
    }
  },
  methods: {
    species: function() {
      const randomN = this.randomNumber();
      let url = "https://swapi.co/api/species/" + randomN + "/";
      axios({ method: "GET", "url": url }).then(result => {
        this.swdata = "Name: " + result.data.name + "   Classification: " + result.data.classification;
        this.swdata1 = "Average Height: " + result.data.average_height + " cm(s) "+ "   Skin Color: "
                + result.data.skin_colors;
      });
    },
    planet: function () {
      const randomN = this.randomNumber();
      let url = "https://swapi.co/api/planets/" + randomN + "/";
      axios({ method: "GET", "url": url }).then(result => {
        this.swdata = "Name: " + JSON.stringify(result.data.name) + "     Terrain: " + result.data.terrain;
        this.swdata1 = "\nDiameter: " + result.data.diameter +" km" + "     Orbital Period: " + result.data.orbital_period
        + " day(s)";
      });
    },
    people: function () {
      const randomN = this.randomNumber();
      let url = "https://swapi.co/api/people/" + randomN + "/";
      axios({ method: "GET", "url": url }).then(result => {
        this.swdata = "Name: " + JSON.stringify(result.data.name) + "     Height: " + result.data.height;
        this.swdata1 = "\nEye Color: " + result.data.eye_color + "     Brith Year: " + result.data.birth_year;
      });
    },
    randomNumber : function(){
      return Math.floor(Math.random() * (10 - 1 + 20)) + 1;
    }
  },
  components: {
    HelloWorld
  },
  mounted() {
    // axios({ method: "GET", "url": "https://swapi.co/api/planets/3/" }).then(result => {
    //   this.swdata = JSON.stringify(result.data);
    // });
    // alert("hello");
    alert("Hello there! The purpose of this website is simple. Since I am quite into StarWar, this werbsite will show " +
            "you some fun facts about StarWar! \n\n(Sorry that it's not very related to rainbow, but I could hardly come up " +
            "with anything interesting about rainbow). \n\nAll information is acquired from The Star War API" +
            "(https://swapi.co/) via RESTful calls. Hope you enjoy it! \n\n-- Zihan Liu");
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
