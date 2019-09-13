<template>
  <div class="about">
    <div style="max-width: 600px">
      <div class="wrapper">
        <label><strong>Readmission Rate (7-Day (adj))</strong></label>
        <bullet-chart
          :max-level="100"
          :sound-level="3.994792"
          :site-level="33.33"
        ></bullet-chart>
      </div>
      <div class="wrapper">
        <bullet-chart
          :max-level="100"
          :sound-level="93.492842"
          :site-level="94.230771"
          :personal-level="95.833331"
        ></bullet-chart>
      </div>
      <div class="wrapper">
        <bullet-chart
          :sound-level="4.2623858"
          :site-level="3.375"
          :personal-level="4"
        ></bullet-chart>
      </div>
      <div class="wrapper">
        <bullet-chart
          :sound-level="2.1148703"
          :site-level="1.9133333"
          :personal-level="1.4878948"
        ></bullet-chart>
      </div>
      <div class="wrapper">
        <bullet-chart
          :sound-level="2.1415279"
          :site-level="1.6222892"
          :personal-level="1.3405882"
        ></bullet-chart>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import BulletChart from "@/components/BulletChart.vue";

export default Vue.extend({
  components: {
    BulletChart,
  },
});
</script>

<style lang="scss" scoped>
.about {
  text-align: left;
}
.wrapper div:first-of-type {
  margin-top: 10px;
  margin-left: 20px;
  margin-right: 20px;
}
.wrapper label {
  text-align: left;
  font-size: 8pt;
}
</style>
