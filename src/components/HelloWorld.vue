<template>
  <v-container>
    <v-row class="text-center" align="center" justify="center">
      <v-app-bar app color="primary" dark>
        <h1>Weather App</h1>
        <v-spacer></v-spacer>
        <v-text-field
          v-model="country"
          class="pt-3"
          @blur="getWeather"
          label="Enter Country"
        ></v-text-field>
      </v-app-bar>
      <v-col v-if="this.weather === null">

      </v-col>
      <v-col v-else cols="6">
        <v-card class="p-5">
          <div align="center" class="mt-5">
            <img
              :src="
                'http://openweathermap.org/img/wn/' +
                this.weather.weather[0].icon +
                '.png'
              "
              alt=""
            />
            <div>
              <h2>{{ this.weather.name }}</h2>
            </div>
            <div>
              <p>Lat {{ this.weather.coord.lat }}</p>
            </div>
            <div>
              <p>Lon {{ this.weather.coord.lon }}</p>
            </div>

            <div>
              <p>{{ this.weather.weather[0].description }}</p>
            </div>
          </div>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",

  data: () => ({
    country: "Nigeria",
    weather: null,
    dailyForcast:null
  }),

  mounted() {
    axios({
      url:
        "http://api.openweathermap.org/data/2.5/weather?q=Nigeria&appid=168b22b6497b371b59f2cfb88691ed86",
      method: "get",
    }).then((response) => {
      // console.log(response.data);
      this.weather = response.data;
    });
  },

  methods: {
    getWeather() {
      axios({
        url:
          "http://api.openweathermap.org/data/2.5/weather?q=" +
          this.country +
          "&appid=168b22b6497b371b59f2cfb88691ed86",
        method: "get",
      }).then((response) => {
        this.weather = response.data;
      });
    },
  },
};
</script>
<style>
input {
  width: 50px !important;
}
</style>
