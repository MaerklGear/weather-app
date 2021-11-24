<template>
  <div class="map skeleton-bg-color"></div>
</template>

<script>
export default {
  name: "MapSkeleton",
};
</script>

<style scoped>
.map {
  flex: 1;
  height: 20rem;
  transform: scale(1);
  animation: pulse 2s infinite;
}
</style>
