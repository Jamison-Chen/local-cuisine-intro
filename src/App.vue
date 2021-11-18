<template>
  <LoadingScreen v-show="isLoading" />
  <h1 id="header-title">農村地方美食小吃特色料理</h1>
  <FilterBar
    :cityTownMap="cityTownMap"
    @update:condition="filterCondition = $event"
  />
  <div id="card-container">
    <Card
      v-for="each in filterMainData"
      :key="each.ID"
      :name="each.Name"
      :hostwords="each.HostWords"
      :city="each.City"
      :town="each.Town"
      :picURL="each.PicURL"
    />
  </div>
  <Footer title="政府資料開放平台" link="https://data.gov.tw/dataset/6037" />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import LoadingScreen from "./components/LoadingScreen.vue";
import Card from "./components/Card.vue";
import FilterBar from "./components/FilterBar.vue";
import Footer from "./components/Footer.vue";

export default defineComponent({
  name: "App",
  components: {
    LoadingScreen,
    FilterBar,
    Card,
    Footer,
  },
  data() {
    return {
      isLoading: true,
      mainData: [],
      filterCondition: { city: "", town: "" },
    };
  },
  methods: {
    async fetchData(): Promise<any> {
      return await fetch(
        "https://data.coa.gov.tw/Service/OpenData/ODwsv/ODwsvTravelFood.aspx"
      ).then((res) => res.json());
    },
  },
  computed: {
    cityTownMap(): any {
      let result: any = {};
      for (let each of this.mainData as any) {
        if (result[each.City] === undefined) {
          result[each.City] = new Set();
          result[each.City].add(each.Town);
        } else result[each.City].add(each.Town);
      }
      return result;
    },
    filterMainData(): any[] {
      return this.mainData.filter(
        (each: any) =>
          each.City.includes(this.filterCondition.city) &&
          each.Town.includes(this.filterCondition.town)
      );
    },
  },
  async created() {
    this.mainData = await this.fetchData();
    this.isLoading = false;
  },
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
#header-title {
  margin: 0;
  padding: 29px 0;
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
