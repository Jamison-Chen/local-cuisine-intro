<template>
  <div id="filter-bar">
    <FilterMenu />
    <FilterMenu />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import FilterMenu from "./FilterMenu.vue";

export default defineComponent({
  components: { FilterMenu },
});
</script>

<style lang="scss" scoped>
#filter-bar {
  background-color: #fff;
  width: 90%;
  margin: 0 auto 15px auto;
  padding: 5px 1.5%;
  border-radius: 5px;
}
</style>
