<template>
  <b-card>
    <b-media>
      <template #aside>
        <b-img height="60" :src="`http://openweathermap.org/img/wn/${forcast.weather[0].icon}@2x.png`"/>
      </template>
      <h3>{{ forcast.temp.max }}º</h3>
      <h3>{{ forcast.temp.min }}</h3>
      <h5>{{ forcast.weather[0].main }}</h5>
    </b-media>
    <h4>{{ forcast.weather[0].description }}</h4>
  </b-card>
</template>

<script>
  export default {
    name: 'weather-card',
    props: [
      'forcast'
    ]
  }
</script>

<style></style>
