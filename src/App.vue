<template>
  <div id="app">
    <Start @hotels="hotels = $event"></Start>
    <HotelSearch :hotels="hotels"></HotelSearch>
  </div>
</template>

<script>
import Start from "./components/Start.vue";
import HotelSearch from "./components/HotelSearch.vue";

export default {
  data() {
    return {
      hotels: {}
    }
  },
  components: {
    Start,
    HotelSearch
  },
};
</script>

<style>
</style>
