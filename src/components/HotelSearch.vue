<template>
  <div>
    <p>hotel検索</p>
    <div>
      <div v-for="hotel in hotels" :key="hotelName(hotel)">
        <a :href="hotelUrl(hotel)">{{hotelName(hotel)}}</a>
        <p>{{hotelSpecial(hotel)}}</p>
        <p>{{hotelAccess(hotel)}}</p>
        <p v-html="hotelReview(hotel)"></p>
      </div>
    </div>
  </div>
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
    hotelReview(info){
        return info.hotel[0].hotelBasicInfo.userReview;
    }
  }
};
</script>