<script>
import axios from 'axios'

export default {
  data: () => ({
    city: '',
    error: '',
    info: null
  }),
  computed: {
    cityName() {
      return '"' + this.city + '"'
    },
    showTime() {
      return 'Time: ' + this.info.location.localtime
    },
    showTemp() {
      return 'Temperature: ' + this.info.current.temp_c
    },
    showCondition(){
      return this.info.current.condition.text
    },
    showFeelsLike() {
      return 'Feels like: ' + this.info.current.feelslike_c
    },
  },
  methods: {
    getWeather() {
      if(this.city.trim().length <= 2) {
        this.error = 'Too short name'
        return false
      }

      this.error = ''

      axios.get(`http://api.weatherapi.com/v1/current.json?key=1946f42dda6b47de9b691118232301&q=${this.city}&aqi=no`)
      .then(res => (this.info = res.data))
    }
  }
}
</script>
8b3a8c178a4e203d944b35b9fc06d5c6
<template>
  <div class="wrapper">
    <h1>Weather App</h1>
    <p>Сheck the weather in {{ city == '' ? 'your city' : cityName }}</p>
    <input 
      type="text" 
      v-model="city" 
      placeholder="Enter your city">
    <button v-if="city!= ''" @click="getWeather()">See the weather</button>
    <button disabled v-else>See the weather</button>
    <p class="error"> {{ error }}</p>
    <div v-if="info != null">
      <p>{{ showTime }}</p>
      <p>{{ showTemp }}</p>
      <p>{{ showCondition }}</p>
      <p>{{ showFeelsLike }}</p>
    </div>
  </div>
</template>

<style scoped>
.error {
  color: #d03939;
}
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #1f0f24;
  text-align: center;
  color: #fff;
}

.wrapper h1 {
margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
margin-top: 30px;
background: transparent;
border: 0;
border-bottom: 2px solid #110813;
color: #fcfcfc;
font-size: 16px;
padding: 5px 8px;
outline: none;
}

.wrapper input:focus {
  border-bottom-color: #62ed7d;
}

.wrapper button:disabled {
  background: #746027;
  cursor: not-allowed;
}

.wrapper button {
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}
</style>
