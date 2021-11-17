<template>
  <LoadingScreen v-show="isLoading" />
  <h1 id="app-title">農村地方美食小吃特色料理</h1>
  <FilterBar />
  <div id="card-container">
    <Card
      v-for="each in mainData"
      :key="each.ID"
      :name="each.Name"
      :hostwords="each.HostWords"
      :city="each.City"
      :town="each.Town"
      :picURL="each.PicURL"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import LoadingScreen from "./components/LoadingScreen.vue";
import Card from "./components/Card.vue";
import FilterBar from "./components/FilterBar.vue";

export default defineComponent({
  name: "App",
  components: {
    LoadingScreen,
    FilterBar,
    Card,
  },
  data() {
    return {
      isLoading: true,
      mainData: [],
    };
  },
  created() {
    fetch("https://data.coa.gov.tw/Service/OpenData/ODwsv/ODwsvTravelFood.aspx")
      .then((resp) => resp.json())
      .then((resp) => {
        this.mainData = resp.slice(0, 21);
        this.isLoading = false;
      });
  },
  methods: {},
});
</script>

<style lang="scss">
body {
  margin: 0;
  background-color: #e9e9e9;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
#app-title {
  margin: 0;
  padding: 35px 0;
  color: #666;
  @media screen and (max-width: 512px) {
    font-size: 1.8rem;
  }
}
#card-container {
  width: 100%;
  display: block;
}
</style>
