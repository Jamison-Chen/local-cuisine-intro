<template>
  <div id="filter-bar">
    <FilterMenu
      :options="new Set(Object.keys(cityTownMap))"
      :placeHolder="'請選擇行政區域...'"
      @update:select="updateSelect('city', $event)"
    />
    <FilterMenu
      :options="selectableTowns"
      :placeHolder="'請選擇鄉鎮區...'"
      @update:select="updateSelect('town', $event)"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import FilterMenu from "./FilterMenu.vue";

export default defineComponent({
  props: {
    cityTownMap: {
      type: Object,
      required: true,
    },
  },
  emits: ["update:condition"],
  components: { FilterMenu },
  data() {
    return {
      citySelected: "",
      townSelected: "",
    };
  },
  computed: {
    selectableTowns(): Set<string> {
      if (this.citySelected in this.cityTownMap) {
        return new Set(this.cityTownMap[this.citySelected]);
      } else return new Set();
    },
  },
  methods: {
    updateSelect(type: "city" | "town", val: string): void {
      if (type === "city") {
        this.citySelected = val in this.cityTownMap ? val : "";
        this.townSelected = "";
      } else if (type === "town") {
        this.townSelected = this.cityTownMap[this.citySelected].has(val)
          ? val
          : "";
      }
      this.$emit("update:condition", {
        city: this.citySelected,
        town: this.townSelected,
      });
    },
  },
});
</script>

<style lang="scss" scoped>
#filter-bar {
  display: inline-block;
  background-color: #fff;
  width: 90%;
  margin: 0 auto 15px auto;
  padding: 12px 1.5%;
  border-radius: 5px;
}
</style>
