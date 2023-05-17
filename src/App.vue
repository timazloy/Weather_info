<script>
import axios from 'axios'

export default {
  data() {
    return {
      city: '',
      error: '',
      info: null
    }
  },
  computed: {
    cityName() {
      return `"${this.city}"`
    }
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "Введите более 2 символов"
        return false
      }

      this.error = ''
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=d4548124d88432ee2fb1c96996ba57de`)
          .then(res => this.info = res.data)
    }
  }
}
</script>

<template>
  <div class="weather">
    <h1 class="weather__title">Погодное приложение</h1>
    <p class="weather__text">Узнать погоду в {{city === "" ? "вашем городе" : cityName}}</p>
    <input class="weather__input" type="text" v-model="city" placeholder="Введите город">
    <button class="weather__button" v-if="city" type="button" @click="getWeather()">Получить погоду</button>
    <button class="weather__button" v-else disabled type="button">Получить погоду</button>
    <p class="weather__error">{{error}}</p>

    <p v-if="info">{{info.main.temp}}</p>
  </div>
</template>

<style scoped>

</style>
