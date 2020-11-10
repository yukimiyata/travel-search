<template>
  <div>
    <p>restaurant検索</p>
    <div>
      <p>{{restaurants[5]}}</p>
      <div v-for="res in restaurants" :key="restaurantName(res)">
        <a :href="restaurantUrl(res)">{{restaurantName(res)}}</a>
        <p>{{restaurantCategory(res)}}</p>
        <p>{{restaurantAccess(res)}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["restaurants"],
  methods: {
    restaurantName(res) {
      return res.name;
    },
    restaurantUrl(res) {
      return res.url;
    },
    restaurantCategory(res) {
      return res.code.category_name_l.join(" : ") + res.code.category_name_s;
    },
    restaurantAccess(res){
        return res.access.line + res.access.station + res.access.station_exit + " " + res.access.walk + "分";
    }
  }
};
</script>