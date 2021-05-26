<template>
  <b-container>
    <b-row>
      <b-link href="https://kinetikoshealth.com" target="_blank">
        <b-img blank-color="#ccc" width="40" height="50"/>
      </b-link>
    </b-row>

    <b-row>
      <b-col>
        <b-media>
          <template #aside>
            <b-img height="128" :src="`http://openweathermap.org/img/wn/${todaysForcast.weather[0].icon}@2x.png`"/>

          </template>
          <h1>{{ todaysForcast.temp }}º</h1>
          <h3>{{ todaysForcast.weather[0].main }}</h3>
        </b-media>
        <h4>{{ todaysForcast.weather[0].description }}</h4>
      </b-col>
    </b-row>

    <b-card-group deck>
      <weather-card v-for="(day, index) in fiveDayForcast" :key="index" :forcast="day"/>
    </b-card-group>
  </b-container>
</template>

<script>
import WeatherCard from '@/components/WeatherCard'

export default {
  name: 'weather',
  components: {
    'weather-card': WeatherCard
  },
  async beforeCreate () {
    const params = {
      lat: '40.20564',
      lon: '-8.41955',
      key: process.env.VUE_APP_API_SECRECT
    }
    try {
      const response = await fetch(`https://api.openweathermap.org/data/2.5/onecall?lat=${params.lat}&lon=${params.lon}&units=metric&appid=${params.key}`)
      if (response.ok) {
        this.apiForcast = await response.json()
      } else {
        console.error('Boom')
      }
    } catch (e) {
      console.error('Boom', e)
    }
  },
  computed: {
    fiveDayForcast () {
      return this.apiForcast.daily.slice(0, 5)
    },
    todaysForcast () {
      return this.apiForcast.current
    }
  },
  data: () => ({
    // forcast: {
    //   temperature: 23,
    //   condition: 'Raining',
    //   description: "It's sunny outside"
    // },
    // calendar: [
    //   { temperature: 23, condition: 'Raining', description: "It's sunny outside" },
    //   { temperature: 23, condition: 'Raining', description: "It's sunny outside" },
    //   { temperature: 23, condition: 'Raining', description: "It's sunny outside" },
    //   { temperature: 23, condition: 'Raining', description: "It's sunny outside" },
    //   { temperature: 23, condition: 'Raining', description: "It's sunny outside" },
    // ],
    apiForcast: []
  })
}
</script>

<style></style>
