<template>
  <div id="app">
    <Slide :closeOnNavigation="true">
      <p @click="setComponent('HotelSearch')" class="hamburger-menu">ホテル</p>
      <p @click="setComponent('RestaurantSearch')" class="hamburger-menu">飲食店</p>
      <p @click="setComponent('Start')" class="hamburger-menu">再検索</p>
    </Slide>

    <template v-if="currentComponent == 'Start'">
      <Start @hotels="hotels = $event" @restaurants="restaurants = $event"></Start>
    </template>
    <template v-else-if="currentComponent == 'HotelSearch'">
      <HotelSearch :hotels="hotels"></HotelSearch>
    </template>
    <template v-else-if="currentComponent == 'RestaurantSearch'">
      <RestaurantSearch :restaurants="restaurants"></RestaurantSearch>
    </template>
  </div>
</template>

<script>
import { Slide } from "vue-burger-menu";
import Start from "./components/Start.vue";
import HotelSearch from "./components/HotelSearch.vue";
import RestaurantSearch from "./components/RestaurantSearch.vue";

export default {
  data() {
    return {
      hotels: {},
      restaurants: {},
      currentComponent: "Start"
    };
  },
  components: {
    Slide,
    Start,
    HotelSearch,
    RestaurantSearch
  },
  methods: {
    setComponent(componentName) {
      this.currentComponent = componentName;
    }
  }
};
</script>

<style>
.hamburger-menu {
  cursor: pointer;
}
</style>
