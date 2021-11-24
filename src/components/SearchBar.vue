<template>
  <form class="search-container" @submit.prevent="onSearchClicked">
    <strong class="post-code-label gray-text">Post Code</strong>
    <input
      :value="postalCode"
      @input="$emit('update:postalCode', $event.target.value)"
      type="text"
      pattern="^\d{3}-\d{4}$|\d{7}$"
      class="post-code-input border"
      placeholder="XXX-XXXX"
    />
    <button class="submit-button ripple" type="submit">
      <strong>submit</strong>
    </button>
  </form>
</template>

<script>
export default {
  name: "SearchBar",
  props: ["postalCode"],

  methods: {
    onSearchClicked() {
      this.$emit("searchClicked");
    },
  },
};
</script>

<style scoped>
.search-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
}

.post-code-input {
  padding: 0.75rem;
  text-align: center;
  color: rgb(0, 0, 0);
  font-size: 1rem;
  outline: none;
  transition: 0.5s;
  border-radius: 0.5rem;
  border: 1px solid rgb(112, 112, 112);
}

.post-code-input:focus,
.post-code-input:hover {
  box-shadow: rgba(73, 73, 73, 0.2) 0px 2px 8px 0px;
  transition: 0.5s;
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
