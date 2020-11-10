<template>
  <v-container>
    <h2>ホテルリスト</h2>
    <template v-for="hotel in hotels">
      <v-row :key="hotelName(hotel)">
        <v-col cols="12" sm="6" md="4" lg="3">
          <a :href="hotelUrl(hotel)">{{hotelName(hotel)}}</a>
        </v-col>
        <v-col cols="12" sm="6" md="4" lg="3">
          <p>{{hotelSpecial(hotel)}}</p>
        </v-col>
        <v-col cols="12" sm="6" md="4" lg="3">
          <p>アクセス：{{hotelAccess(hotel)}}</p>
        </v-col>
        <v-col cols="12" sm="6" md="4" lg="3">
          <p v-html="hotelReview(hotel)"></p>
        </v-col>
      </v-row>
    </template>
  </v-container>
</template>

<script>
export default {
  props: ["hotels"],
  methods: {
    hotelName(info) {
      return info.hotel[0].hotelBasicInfo.hotelName;
    },
    hotelUrl(info) {
      return info.hotel[0].hotelBasicInfo.hotelInformationUrl;
    },
    hotelSpecial(info) {
      return info.hotel[0].hotelBasicInfo.hotelSpecial;
    },
    hotelAccess(info) {
      return info.hotel[0].hotelBasicInfo.access;
    },
    hotelReview(info) {
      return info.hotel[0].hotelBasicInfo.userReview;
    }
  }
};
</script>