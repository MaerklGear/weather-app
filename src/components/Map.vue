<template>
  <div ref="mapDiv" class="map skeleton-bg-color shadow"></div>
</template>

<script>
/* eslint-disable no-undef */
import { Loader } from "@googlemaps/js-api-loader";
import { onMounted, ref } from "@vue/runtime-core";
const GOOGLE_MAPS_API_KEY = "AIzaSyCL8vsEG-itIMwRSZSFiFUkrwUEPeZaweA";

export default {
  name: "Map",
  props: ["lat", "lon"],

  setup(props) {
    if (!props.lat && !props.lon) return;
    const loader = new Loader({ apiKey: GOOGLE_MAPS_API_KEY });
    const mapDiv = ref(null);
    onMounted(async () => {
      await loader.load();
      new google.maps.Map(mapDiv.value, {
        center: { lat: props.lat, lng: props.lon },
        zoom: 12,
      });
    });
    return { mapDiv };
  },
};
</script>

<style scoped>
.map {
  flex: 1;
  height: 20rem;
  border-radius: 0.5rem;
}
</style>
