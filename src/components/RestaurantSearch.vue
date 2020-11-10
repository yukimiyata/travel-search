<template>
  <v-container>
    <h2>飲食店リスト</h2>
    <template v-for="res in restaurants">
      <v-row :key="restaurantName(res)">
        <v-col cols="12" sm="6" md="4" lg="3">
          <a :href="restaurantUrl(res)">{{restaurantName(res)}}</a>
        </v-col>
        <v-col cols="12" sm="6" md="4" lg="3">
          <p>{{restaurantCategory(res)}}</p>
        </v-col>
        <v-col cols="12" sm="6" md="4" lg="3">
          <p>アクセス：{{restaurantAccess(res)}}</p>
        </v-col>
      </v-row>
    </template>
  </v-container>
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
    restaurantAccess(res) {
      return (
        res.access.line +
        res.access.station +
        res.access.station_exit +
        " " +
        res.access.walk +
        "分"
      );
    }
  }
};
</script>

<style scoped>
</style>