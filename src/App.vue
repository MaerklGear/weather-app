<template>
  <div class="app">
    <div class="page-wrapper">
      <SearchBar
        v-model:postalCode="postalCode"
        @searchClicked="onSearchClicked"
      />
      <transition name="fade">
        <div v-if="forecastIsLoaded()">
          <h2>{{ forecasts.city_name }}, {{ forecasts.country_code }}</h2>
          <strong class="gray-text">{{ days }}-day forecast</strong>
          <div class="horizontal-wrapper">
            <WeatherBox
              v-for="forecast in forecasts.data"
              :key="forecast"
              :forecast="forecast"
            />
          </div>
          <div class="horizontal-wrapper">
            <Map :lat="Number(forecasts.lat)" :lon="Number(forecasts.lon)" />
            <Recommendations
              @locationRecommendationClicked="onLocationRecommendationClicked"
            />
          </div>
        </div>
      </transition>
      <transition name="fade">
        <div v-if="loading">
          <div class="text-skeleton skeleton-bg-color"></div>

          <div class="text-skeleton skeleton-bg-color"></div>
          <div class="horizontal-wrapper">
            <WeatherBoxSkeleton v-for="skeleton in days" :key="skeleton" />
          </div>

          <div class="horizontal-wrapper">
            <MapSkeleton></MapSkeleton>
            <MapSkeleton></MapSkeleton>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import WeatherBox from "./components/WeatherBox.vue";
import WeatherBoxSkeleton from "./components/WeatherBoxSkeleton.vue";
import Map from "./components/Map.vue";
import MapSkeleton from "./components/MapSkeleton.vue";
import Recommendations from "./components/Recommendations.vue";

const API_URL = "https://api.weatherbit.io/v2.0/forecast/daily?";
const WEATHER_API_KEY = "23d2ea5fb4f94f1d992113e57b52df09";
export default {
  components: {
    SearchBar,
    WeatherBox,
    WeatherBoxSkeleton,
    Map,
    MapSkeleton,
    Recommendations,
  },
  name: "App",
  data() {
    return {
      loading: false,
      forecasts: {},
      postalCode: "160-0022",
      country: "jp",
      days: 3,
    };
  },

  methods: {
    forecastIsLoaded() {
      return !!this.forecasts?.data;
    },
    async onSearchClicked() {
      this.loading = true;
      this.forecasts = {};

      const forecastsResponse = await fetch(
        `${API_URL}postal_code=${this.postalCode}&country=${this.country}&days=${this.days}&key=${WEATHER_API_KEY}`
      );
      const forecastsBody = await forecastsResponse.json();
      this.forecasts = forecastsBody;
      this.loading = false;
    },
    async onLocationRecommendationClicked(recommendation) {
      this.postalCode = recommendation.postalCode;
      this.onSearchClicked(recommendation.postalCode);
    },
  },
};
</script>

<style>
* {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

html {
  background-color: #f8f8f8;
}

.app {
  display: flex;
  justify-content: center;
}

.page-wrapper {
  display: flex;
  flex-direction: column;
  padding: 2rem;
  max-width: 720px;
  width: 100%;
  border-radius: 0.5rem;
}

.horizontal-wrapper {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  padding-top: 2rem;
  padding-bottom: 2rem;
  gap: 1rem;
}

.post-code-label {
  margin-right: 1rem;
}

.text-skeleton {
  width: 50%;
  height: 1.8rem;
  line-height: 140%;
  margin-top: 0.5rem;
  transform: scale(1);
  animation: pulse 2s infinite;
}
.skeleton-bg-color {
  background-color: #eaeaea;
}

.gray-text {
  color: #767676;
}

.shadow {
  box-shadow: rgb(73 73 73 / 20%) 0px 2px 8px 0px;
}

.box {
  border-radius: 0.5rem;
  display: flex;
  padding: 1.5rem;
  min-width: 10rem;
  flex-direction: column;
  align-items: center;
  background-color: #fff;
}

@media only screen and (max-width: 780px) {
  .horizontal-wrapper {
    justify-content: center;
    gap: 2rem;
  }

  .box {
    flex: 1;
  }
  .submit-button {
    width: 100%;
  }
  .post-code-input {
    flex: 1;
    margin-top: 0.5rem;
    margin-bottom: 0.5rem;
  }
  .map {
    min-width: 100%;
  }
}

@keyframes pulse {
  0% {
    transform: scale(0.99);
    box-shadow: 0 0 0 0 rgba(0, 0, 0, 0.4);
  }

  50% {
    transform: scale(1);
    box-shadow: 0 0 0 2px rgba(0, 0, 0, 0);
  }

  100% {
    transform: scale(0.99);
    box-shadow: 0 0 0 0 rgba(0, 0, 0, 0);
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
