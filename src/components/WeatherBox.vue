<template>
  <div class="box shadow">
    <img class="icon" :src="`${icon_url}${forecast.weather.icon}.png`" />
    <span>{{ readableDate(forecast.datetime) }}</span>
    <h4>{{ forecast.weather.description }}</h4>
    <span class="gray-text"
      >Max: <strong> {{ forecast.max_temp }}° </strong>Min:
      <strong>{{ forecast.min_temp }}°</strong></span
    >
  </div>
</template>

<script>
export default {
  name: "WeatherBox",
  props: {
    forecast: {},
  },
  methods: {
    readableDate(datetime) {
      return new Date(datetime).toDateString();
    },
  },
  data() {
    return {
      icon_url: "https://www.weatherbit.io/static/img/icons/",
    };
  },
};
</script>

<style scoped>
.icon {
  width: 120px;
  height: 120px;
}
</style>
