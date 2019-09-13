<template>
  <svg width="100%" height="65px">
    <svg preserveAspectRatio="none" viewBox="0 0 100 100">
      <rect class="bg" fill="#ccc" width="100%" height="40"></rect>
      <rect class="data" fill="#0074d9" :width="parentData" height="40"></rect>
      <rect
        class="data"
        fill="#000"
        :width="childData"
        y="16"
        height="8"
      ></rect>
      <g class="markers">
        <line x1="0.25" y1="0" x2="0.25" y2="50"></line>
        <line x1="25%" y1="0" x2="25%" y2="50"></line>
        <line x1="50%" y1="0" x2="50%" y2="50"></line>
        <line x1="75%" y1="0" x2="75%" y2="50"></line>
        <line x1="99.75" y1="0" x2="99.75" y2="50"></line>
      </g>
    </svg>
    <g text-anchor="middle">
      <text text-anchor="start" fill="#0074d9" x="0" y="60">0%</text>
      <text fill="#0074d9" x="25%" y="60">25%</text>
      <text fill="#0074d9" x="50%" y="60">50%</text>
      <text fill="#0074d9" x="75%" y="60">75%</text>
      <text text-anchor="end" fill="#0074d9" x="100%" y="60">100%</text>
    </g>
  </svg>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  props: {
    dataSet: {
      required: true
    }
  },
  computed: {
    parentData(): string {
      return "45%";
    },
    childData(): string {
      return "38%";
    }
  }
});
</script>

<style lang="scss" scoped>
svg {
  min-width: 320px;
}

line {
  stroke: #666;
  stroke-width: 0.5;
  /*   vector-effect: non-scaling-stroke; */
}
</style>
