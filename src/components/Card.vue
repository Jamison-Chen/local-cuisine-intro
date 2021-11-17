<template>
  <div
    class="card"
    :style="`background-image:url(${picURL})`"
    @mouseenter="isHovered = true"
    @mouseleave="isHovered = false"
  >
    <div class="city-tag">{{ city }}</div>
    <div class="bottom-part" :class="{ active: isHovered }">
      <div class="town-tag">{{ town }}</div>
      <div class="name-tag">{{ name }}</div>
      <div class="divide-line"></div>
      <div class="hostwords-tag">
        {{ hostwords.slice(0, 50) }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: ["name", "hostwords", "picURL", "city", "town"],
  data() {
    return {
      isHovered: false,
    };
  },
});
</script>

<style lang="scss" scoped>
.card {
  position: relative;
  width: 370px;
  height: 200px;
  margin: 15px;
  @media screen and (max-width: 512px) {
    margin: 2px;
  }
  display: inline-flex;
  flex-direction: column;
  justify-content: flex-end;
  text-align: start;
  overflow: hidden;
  background-size: 100%;
  transition-duration: 1000ms;
  color: #fff;
  &::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 0;
    background: linear-gradient(
      0deg,
      rgba(0, 0, 0, 0.8) 0%,
      rgba(0, 0, 0, 0.1) 50%
    );
    background: -moz-linear-gradient(
      0deg,
      rgba(0, 0, 0, 0.8) 0%,
      rgba(0, 0, 0, 0.1) 50%
    );
    background: -webkit-linear-gradient(
      0deg,
      rgba(0, 0, 0, 0.8) 0%,
      rgba(0, 0, 0, 0.1) 50%
    );
    background: -o-linear-gradient(
      0deg,
      rgba(0, 0, 0, 0.8) 0%,
      rgba(0, 0, 0, 0.1) 50%
    );
  }
  &:hover {
    background-size: 105%;
    background-position: 50%;
  }
}
.city-tag {
  position: absolute;
  top: 0;
  left: 0;
  height: fit-content;
  width: fit-content;
  background-color: #ffae00;
  font-size: 0.8rem;
  font-weight: 600;
  padding: 3px;
}
.bottom-part {
  position: absolute;
  bottom: -60px;
  z-index: 100;
  transition-duration: 300ms;
  &.active {
    bottom: 0;
  }
  & > .town-tag {
    font-style: italic;
    font-size: 0.8rem;
    padding-left: 10px;
  }
  & > .name-tag {
    padding: 0 0 10px 10px;
  }
  & > .divide-line {
    width: 50px;
    height: 3px;
    margin-left: 10px;
    background-color: #fff;
  }
  & > .hostwords-tag {
    font-size: 0.8rem;
    padding: 10px;
    height: 37px;
  }
}
</style>
