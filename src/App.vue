<template>
  <div id="app">
    <Start @hotels="hotels = $event" @restaurants="restaurants = $event"></Start>
    <RestaurantSearch :restaurants="restaurants"></RestaurantSearch>
    <HotelSearch :hotels="hotels"></HotelSearch>
  </div>
</template>

<script>
import Start from "./components/Start.vue";
import HotelSearch from "./components/HotelSearch.vue";
import RestaurantSearch from "./components/RestaurantSearch.vue"

export default {
  data() {
    return {
      hotels: {},
      restaurants: {}
    }
  },
  components: {
    Start,
    HotelSearch,
    RestaurantSearch
  },
};
</script>

<style>
</style>
