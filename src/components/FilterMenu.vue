<template>
  <select
    id="filter-menu"
    @change="$emit('update:select', $event.target.value)"
  >
    <option :value="placeHolder" selected>{{ placeHolder }}</option>
    <option v-for="each in options" :key="each" :value="each">
      {{ each }}
    </option>
  </select>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    options: {
      type: Set,
      required: true,
    },
    placeHolder: {
      type: String,
      default: "",
    },
  },
  emits: ["update:select"],
});
</script>

<style lang="scss" scoped>
#filter-menu {
  display: inline;
  height: 35px;
  width: 90%;
  max-width: 300px;
  margin: 8px 15px;
  border: none;
  border-radius: 3px;
  background-color: #e9e9e9;
  padding: 0 10px;
  font-size: 1rem;
  & > option {
    background-color: #fff;
    width: 300px;
    font-size: 0.8rem;
  }
}
</style>
