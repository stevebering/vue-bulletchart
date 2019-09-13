<template>
<div>
  <svg width="100%" height="65px">
    <svg preserveAspectRatio="none" viewBox="0 0 100 100">
      <rect class="bg" width="100%" :height="barHeight"></rect>
      <rect 
        class="site-level" 
        v-if="siteLevel" 
        :width="siteLevelPercentage" 
        :height="barHeight">
        <title>{{siteLevel && siteLevel.toFixed(2)}}</title>
      </rect>
      <rect 
        class="personal-level" 
        v-if="personalLevel"
        :width="personalLevelPercentage" 
        height="16" 
        y="12">
        <title>{{personalLevel && personalLevel.toFixed(2)}}</title>
      </rect>
      <line 
        class="sound-level" 
        v-if="soundLevel" 
        :x1="soundLevelPercentage" 
        y1="5" 
        :x2="soundLevelPercentage" 
        y2="35">
        <title>{{soundLevel && soundLevel.toFixed(2)}}</title>
      </line>
      <!-- <rect 
        class="sound-level" 
        v-if="soundLevel" 
        :x="soundLevelPercentage"
        width="1px" 
        :height="barHeight"
      >
        <title>{{soundLevel}}</title>
      </rect> -->
      <g class="markers">
        <line v-for="increment in increments" 
          :key="increment.position" 
          :x1="increment.position" 
          :x2="increment.position" 
          y1="45" 
          y2="60">
        </line>
      </g>
    </svg>
    <g text-anchor="middle">
      <text 
        v-for="increment in increments" 
        :key="increment.position" 
        :text-anchor="increment.anchor" 
        :x="formatAsPercentage(increment.position)"
        font-size=10
        y="50"
        class="label">
        {{ increment.label }}
      </text>
    </g>
  </svg>
</div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  props: {
    maxLevel: {
      type: Number
    },
    partitions: {
      type: Number,
      default: 5
    },
    siteLevel: {
      type: Number
    },
    personalLevel: {
      type: Number
    },
    soundLevel: {
      type: Number
    }
  },
  data() {
    return {
      barHeight: 40
    };
  },
  computed: {
    // if the maxLevel is an explicit number, use that as our max level. Otherwise, calculate it based on the maximum value provided to the chart
    actualMaxLevel(): number {
      const maxValue = Math.max(this.siteLevel || 0, this.personalLevel || 0, this.soundLevel || 0);
      if (this.maxLevel && typeof this.maxLevel === "number") {
        return Math.max(this.maxLevel, Math.ceil(maxValue));
      }
      return Math.ceil(maxValue);
    },

    siteLevelPercentage(): string {
      let value = (this.siteLevel/this.actualMaxLevel) * 100;
      return `${value.toString()}%`;
    },
    
    personalLevelPercentage(): string {
      let value = (this.personalLevel/this.actualMaxLevel) * 100;
      return `${value.toString()}%`;
    },
    
    soundLevelPercentage(): string {
      let value = (this.soundLevel/this.actualMaxLevel) * 100;
      return `${value.toString()}%`;
    },
    
    increments(): Array<{ position: number, label: string, anchor?: string }> {
      let values: Array<{position: number, label: string, anchor?: string}> = [];
      values.push({ position: 0.25, label: "0", anchor: "start" });
      
      // use the number of partitions provided, unless the partitions is larger than our largest number
      // we don't want to end up with fractions in the labels
      let actualPartitions = Math.min(this.partitions, Math.round(this.actualMaxLevel));

      for (let i = 1; i < actualPartitions; i++) {
        let position = (100 / actualPartitions) * i;
        let label = (this.actualMaxLevel / actualPartitions) * i;
        values.push({position: position, label: Math.round(label).toString() });
      }

      // insert the last position statically at 0.25 from the end
      values.push( { position: 99.75, label: this.actualMaxLevel.toString(), anchor: "end" });

      return values;
    }
  },
  methods: {
    formatAsPercentage(value: number) : string {
      return `${value.toString()}%`;
    }
  }
});
</script>

<style lang="scss" scoped>
svg {
  min-width: 100px;
}

.markers > line {
  stroke: #888;
  stroke-width: 0.5;
}

.bg {
  fill: #D2D2D2;
}

.sound-level {
  stroke: #000;
  stroke-width: 0.5;
}

.site-level {
  fill: #FAA424;
}

.personal-level {
  fill: #2E75B6
}

.label {
  fill: #000;
  font-size: 10;
}
</style>
