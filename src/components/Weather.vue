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
            <b-img height="128" blank-color="#ccc"/>
          </template>
          <h1>{{ apiForcast.current.temp }}º</h1>
          <h3>{{ apiForcast.current.weather[0].main }}</h3>
        </b-media>
        <h4>{{ apiForcast.current.weather[0].description }}</h4>
      </b-col>
    </b-row>

    <b-card-group deck>
      <weather-card v-for="(day, index) in apiForcast.daily" :key="index" :forcast="day"/>
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
  async mounted () {
    const apiKey = process.env.VUE_APP_API_SECRECT

    const location = {
      lat: '40.20564',
      lon: '-8.41955'
    }

    try {
      const response = await fetch(`https://api.openweathermap.org/data/2.5/onecall?lat=${location.lat}&lon=${location.lon}&units=metric&appid=${apiKey}`)
      if (response.ok) {
        const text = await response.json()
        this.apiForcast = text
      } else {
        console.error('boom')
      }
    } catch (e) {
      console.error('error', e)
    }
  },
  data: () => ({
    forcast: {
      temperature: 23,
      condition: 'Raining',
      description: "It's sunny outside"
    },
    calendar: [
      { temperature: 23, condition: 'Raining', description: "It's sunny outside" },
      { temperature: 23, condition: 'Raining', description: "It's sunny outside" },
      { temperature: 23, condition: 'Raining', description: "It's sunny outside" },
      { temperature: 23, condition: 'Raining', description: "It's sunny outside" },
      { temperature: 23, condition: 'Raining', description: "It's sunny outside" },
    ],
    apiForcast: []
  })
}
</script>

<style></style>
