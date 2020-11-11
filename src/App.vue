<template>
  <v-app>
    <v-navigation-drawer app v-model="drawer" clipped>
      <v-container>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="title grey--text text--darken-2">メニュー</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-divider></v-divider>
        <v-list dense nav>
          <template v-for="nav_list in nav_lists">
            <v-list-item :key="nav_list.name">
              <v-list-item-content>
                <v-list-item-title
                  @click="currentComponent = nav_list.valu; drawer=!drawer;"
                  class="hamburger-menu"
                >{{ nav_list.name }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </template>
        </v-list>
      </v-container>
    </v-navigation-drawer>
    <v-app-bar color="green" dark app clipped-left>
      <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>現在地からホテルと飲食店検索！</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-dialog v-model="dialog" width="500">
          <template v-slot:activator="{ on, attrs }">
            <v-btn v-bind="attrs" v-on="on" text>使い方</v-btn>
          </template>
          <v-card>
            <v-card-title class="headline green lighten-2">現在地からホテルと飲食店検索</v-card-title>
            <v-card-text>距離を選んで検索ボタンを押すと近くの飲食店とホテル(当日の空室)が検索できます！ホテル(楽天)飲食店(ぐるなび)</v-card-text>
            <v-divider></v-divider>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="dialog = false">閉じる</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar-items>
    </v-app-bar>
    <v-main>
      <template v-if="currentComponent == 'Start'">
        <Start
          @hotels="hotels = $event"
          @restaurants="restaurants = $event"
          @goToHotelPage="currentComponent = $event"
        ></Start>
      </template>
      <template v-else-if="currentComponent == 'HotelSearch'">
        <HotelSearch :hotels="hotels"></HotelSearch>
      </template>
      <template v-else-if="currentComponent == 'RestaurantSearch'">
        <RestaurantSearch :restaurants="restaurants"></RestaurantSearch>
      </template>
    </v-main>
    <v-footer color="green" dark app>ホテルと飲食店検索アプリ</v-footer>
  </v-app>
</template>

<script>
import Start from "./components/Start.vue";
import HotelSearch from "./components/HotelSearch.vue";
import RestaurantSearch from "./components/RestaurantSearch.vue";
export default {
  name: "App",
  data() {
    return {
      hotels: {},
      restaurants: {},
      currentComponent: "Start",
      drawer: null,
      nav_lists: [
        { name: "ホテル", valu: "HotelSearch" },
        { name: "飲食店", valu: "RestaurantSearch" },
        { name: "検索", valu: "Start" }
      ],
      dialog: false
    };
  },
  components: {
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
