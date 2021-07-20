<template>
  <v-app id="inspire">
    <v-card elevation="2">
      {{store.name}}
    </v-card>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    drawer: null,
    isLoading: false,
    store: null,
  }),

  created() {
    axios
      .get(
        "https://api.openweathermap.org/data/2.5/weather?q=London&appid=36b30956cad8e4c85834f1a46cb61dec"
      )
      .then((res) => {
        console.log(res.data);
        this.store = res.data;
        this.isLoading = true;
      });
  },
};
</script>
