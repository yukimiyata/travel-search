<template>
  <div>
    <button @click="start">start</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      latitude: 0,
      longitude: 0,
      hotelRange: 3
    };
  },
  methods: {
    start() {
      navigator.geolocation.getCurrentPosition(this.success, this.error);
    },
    success(position) {
      this.latitude = position.coords.latitude;
      this.longitude = position.coords.longitude;
      this.searchHotel(this.latitude, this.longitude);
    },
    error() {
      //エラー時の処理を実装途中
      console.log("error");
    },
    searchHotel(latitude, longitude) {
      console.log(latitude);
      console.log(longitude);
      axios
        //datumType=2を１に変更して、経度緯度を変数に置き換える
        .get(
          "https://app.rakuten.co.jp/services/api/Travel/VacantHotelSearch/20170426?applicationId=1096600551356603387&format=json&datumType=2&latitude=" +
            "128440.51" +
            "&longitude=" +
            "503172.21" +
            "&searchRadius=" +
            this.hotelRange
        )
        .then(response => this.$emit("hotels", response.data.hotels))
        .catch(error => {
          console.log(error);
          // this.errored = true;
        });
    }
  }
};
</script>