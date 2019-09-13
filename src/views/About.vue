<template>
  <div class="about">
    <h1>This is an about page</h1>
    <bullet-chart></bullet-chart>
    <div style="max-width: 100px">
      <bullet-chart></bullet-chart>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import BulletChart from "@/components/BulletChart.vue";

export default Vue.extend({
  components: {
    BulletChart
  }
});
</script>
