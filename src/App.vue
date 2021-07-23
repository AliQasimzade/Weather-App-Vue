<template>
  <v-app ref="app">
    <v-container ref="cont">
      <v-form>
        <v-text-field label="Search..." filled rounded dense></v-text-field>
        <v-btn class="mx-2" fab dark color="green">
          <v-icon>{{ icons.mdiMagnify }}</v-icon>
        </v-btn>
      </v-form>
      <div class="city-weather" v-if="isLoading">
        <h2>Weather in {{ store.name }}</h2>
        <h3>{{ Math.abs(273.15 - store.main.temp).toPrecision(2) }} °C</h3>
        <img :src="image" alt="image" v-if="isLoading" width="60" />
        <h3>{{ store.weather[0].description }}</h3>
        <h3>Humidity: {{ store.main.humidity }} %</h3>
        <h3>Wind speed: {{ store.wind.speed }} km/h</h3>
        <h3>{{ test }}</h3>
      </div>
    </v-container>
  </v-app>
</template>
<script>
import axios from "axios";

import { mdiMagnify } from "@mdi/js";
import "@mdi/font/css/materialdesignicons.css";

export default {
  data: () => ({
    isLoading: false,
    store: null,
    image: "",
    icons: {
      mdiMagnify,
    },
    test: "Ali",
  }),
 
  created() {
    axios
      .get(
        "https://api.openweathermap.org/data/2.5/weather?q=London&appid=36b30956cad8e4c85834f1a46cb61dec"
      )
      .then((res) => {
        this.store = res.data;
        this.isLoading = true;
        this.image = `https://openweathermap.org/img/wn/${res.data.weather[0].icon}@2x.png`;
        this.test = this.$store.getters.getName
      });

    axios
      .get(
        "https://api.unsplash.com/search/photos?query=London&client_id=5aualamt2KC7W-6LD_lWJYCZazwNlUMrQ6-KkH3wo9Y"
      )
      .then((res) => {
        document.getElementById(
          "app"
        ).style.backgroundImage = `url(${res.data.results[0].urls.full})`;
      });
  },
};
</script>

<style>
#app {
  height: 100vh !important;
  background-repeat: no-repeat;
  background-size: cover;
}
.v-application--wrap {
  display: flex;
  align-items: center;
  justify-content: center;
}
.city-weather {
  width: 95%;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  flex-direction: column;
  color: #fff !important;
}
h3 {
  margin: 4px;
}
form {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  margin-bottom: 30px !important;
}
.container {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  flex-direction: column;
  background: linear-gradient(to right, #0f2027, #203a43, #2c5364);
  border-radius: 8px;
  height: fit-content;
  width: 500px !important;
}
.v-text-field__details {
  display: none !important;
}
.v-input {
  flex: 1 !important;
}
input {
  color: #ccc !important;
}

.v-input__control {
  border: 1px solid green !important;
}

.v-form .ma-2 {
  margin-top: 0 !important;
}
</style>
