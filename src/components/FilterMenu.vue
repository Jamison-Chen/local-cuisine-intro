<template>
  <select id="filter-menu">
    <option value=""></option>
  </select>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    options: {
      type: Array,
      default: [],
    },
  },
});
</script>

<style lang="scss" scoped>
#filter-menu {
  display: inline;
  height: 35px;
  width: 26%;
  margin: 15px;
  border: none;
  border-radius: 3px;
  background-color: #e9e9e9;
  & > option {
    background-color: #fff;
  }
}
</style>
