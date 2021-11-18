<template>
  <div id="footer">
    <div id="footer-title">{{ title }}</div>
    <a id="footer-link" :href="link" target="_blank">{{ link }}</a>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    title: {
      type: String,
      required: true,
    },
    link: {
      type: String,
      required: true,
    },
  },
});
</script>

<style lang="scss" scoped>
#footer {
  margin: 15px 0;
}
#footer-title {
  font-weight: bold;
  color: #999;
}
#footer-link {
  color: #666;
}
</style>
