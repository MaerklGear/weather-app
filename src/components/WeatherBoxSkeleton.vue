<template>
  <div class="box shadow">
    <img class="icon" src="../assets/image.svg" />
    <span class="text-skeleton skeleton-bg-color"></span>
    <h4 class="text-skeleton skeleton-bg-color"></h4>
    <span class="text-skeleton skeleton-bg-color"></span>
  </div>
</template>

<script>
export default {
  name: "WeatherBoxSkeleton",
};
</script>

<style scoped>
.icon {
  width: 120px;
  height: 120px;
}
</style>
