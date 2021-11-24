<template>
  <div class="box shadow">
    <strong>Popular Locations</strong>
    <div class="horizontal-wrapper">
      <button
        v-for="recommendation in recommendations"
        :key="recommendation"
        class="submit-button ripple"
        @click="onLocationClicked(recommendation)"
      >
        <strong>{{ recommendation.displayName }}</strong>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Recommendations",
  data() {
    return {
      recommendations: [
        { displayName: "Tokyo", postalCode: "160-0022", country: "jp" },
        { displayName: "Osaka", postalCode: "543-0062", country: "jp" },
        { displayName: "Kobe", postalCode: "650-8567", country: "jp" },
        { displayName: "Yokohama", postalCode: "221-0057", country: "jp" },
        { displayName: "Nagoya", postalCode: "450-0005", country: "jp" },
        { displayName: "Okinawa", postalCode: "904-0022", country: "jp" },
      ],
    };
  },
  methods: {
    onLocationClicked(recommendation) {
      this.$emit("locationRecommendationClicked", {
        postalCode: recommendation.postalCode,
        country: recommendation.country,
      });
    },
  },
};
</script>

<style scoped>
.box {
  flex: 1;
  min-height: 17rem;
  align-items: baseline;
}

.submit-button {
  border-radius: 0.5rem;
  border: 1px solid #3b82f6;
  padding: 0.75rem;
  color: white;
  background-color: #3b82f6;
}

.ripple {
  background-position: center;
  transition: background 0.8s;
}
.ripple:hover {
  background: #47a7f5 radial-gradient(circle, transparent 1%, #47a7f5 1%)
    center/15000%;
}
.ripple:active {
  background-color: #6eb9f7;
  background-size: 100%;
  transition: background 0s;
}
</style>
