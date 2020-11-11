<template>
  <v-container>
    <v-row justify="center" align-content="center">
      <v-col cols="12" sm="6" md="4" lg="3">
        <h3>ホテル検索</h3>
        <v-select :items="hotelRange" label="現在地からの距離(km)" v-model="hotelKm"></v-select>
      </v-col>
      <v-col cols="12" sm="6" md="4" lg="3">
        <h3>飲食店検索</h3>
        <v-select
          :items="restaurantRange"
          item-text="km"
          item-value="id"
          label="現在地からの距離(km)"
          v-model="restaurantKm"
        ></v-select>
      </v-col>
    </v-row>
    <v-row justify="center" align-content="center">
      <v-col cols="2" sm="1" md="1" lg="1">
        <v-btn @click="start" elevation="2" :loading="loading" x-large>検索</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      latitude: 0,
      longitude: 0,
      hotelRange: [3, 2, 1],
      hotelKm: 3,
      restaurantRange: [
        { km: 3, id: 5 },
        { km: 2, id: 4 },
        { km: 1, id: 3 },
        { km: 0.5, id: 2 },
        { km: 0.3, id: 1 }
      ],
      restaurantKm: 5,
      loading: false
    };
  },
  methods: {
    start() {
      this.loading = true;
      navigator.geolocation.getCurrentPosition(this.success, this.error);
    },
    success(position) {
      this.latitude = position.coords.latitude;
      this.longitude = position.coords.longitude;
      this.searchHotel(this.latitude, this.longitude);
      this.searchRestaurant(this.latitude, this.longitude);
      this.loading = false;
      // this.$emit("goToHotelPage", "HotelSearch");
    },
    error() {
      //エラー時の処理を実装途中
      console.log("error");
    },
    searchHotel(latitude, longitude) {
      console.log(latitude);
      console.log(longitude);
      axios
        .get(
          "https://app.rakuten.co.jp/services/api/Travel/VacantHotelSearch/20170426?applicationId=1096600551356603387&format=json&datumType=1&latitude=" +
            this.latitude +
            "&longitude=" +
            this.longitude +
            "&searchRadius=" +
            this.hotelKm
        )
        .then(response => this.$emit("hotels", response.data.hotels))
        .catch(error => {
          console.log(error);
          // this.errored = true;
        });
    },
    searchRestaurant(latitude, longitude) {
      console.log(latitude);
      console.log(longitude);
      axios
        .get(
          "https://api.gnavi.co.jp/RestSearchAPI/v3/?keyid=6c49b3965739725d4125a037706ae02a",
          {
            params: {
              latitude: this.latitude,
              longitude: this.longitude,
              range: this.restaurantKm
            }
          }
        )
        .then(response => this.$emit("restaurants", response.data.rest))
        .catch(error => {
          console.log(error);
          // this.errored = true;
        });
    }
  }
};
</script>