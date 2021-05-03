import { axios } from '@/plugins/axios'
<template>
  <q-page class="flex column">
      <div class="col">
        <q-input
          v-model="search"
          placeholder="Search"
          borderless
          >
        <template v-slot:before>
          <q-icon
          @click="getLocation"
            name="my_location" />
        </template>

        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
      </div>

      <template v-if="WeatherData">
      <div class="text-black text-center">

        <div class="text-h4 text-weight-dark">
          Khandwa
        </div>

        <div class="text-black text-center text-h6 text weight-light">
          Rain
        </div>

        <div class="text-h1 text-weight-thin q-my-lg relative-position">
          <span>8</span>
          <span class="text-h4 relative-position degree">&deg;C</span>
        </div>

      </div>

      <div class="col text-center">
      </div>
      </template>

      <template v-else>
        <div class="col column text-center text-black">
          <div class="col text-h2 text-weight-thick">
            Quasar<br>Weather
          </div>
          <q-btn
            @click="getLocation"
            class="col"
            flat
            >
            <q-icon left size="3em" name="my_location" />
            <div>Find My Location</div>
          </q-btn>
        </div>
      </template>

      <div class="col skyline"></div>

  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      search: '',
      weatherData: null,
      lat: null,
      lon: null,
      apiUrl: 'https://api.openweathermap.org/data/2.5/weather',
      apiKey: '59b7ef44b63ae2fe52bd9715c8a54f3d'
    }
  },
  methods: {
    getLocation () {
      navigator.geolocation.getCurrentPosition(position => {
        console.log('position: ', position)
        this.lat = position.coords.latitude
        this.lon = position.coords.longitude
        this.getWeatherByCoords()
      })
    },
    getWeatherByCoords () {
      this.$axios.get(`${this.apiUrl}?lat=${this.lat}&lon=${this.lon}&appid=${this.apiKey}&units=metric`).then(response => {
        console.log('response: ', response)
      })
    }
  }
}
</script>

<style lang="sass">
  .q-page
    background:linear-gradient(to bottom,#136a8a, #267871)
  .degree
    top: -45px
  .skyline
    flex: 0 0 150px
    background: url(../statics/skyline.png)
    background-size: contain
    background-position: center bottom
</style>
