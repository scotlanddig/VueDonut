<template>
        <span>
        <figure>
            <svg width="80" height="80" viewBox="0 0 42 42" class="donut" aria-labelledby="beers-title beers-desc" role="img">
                <title>ENPS Title</title>
                <desc></desc>
                <title>{{dataTitle}}</title>
                <circle class="donut-hole" :cx="cx" :cy="cy" :r="radius" fill="transparent"></circle>
                <circle class="donut-ring" :cx="cx" :cy="cy" :r="radius" fill="transparent" :stroke="ringColour" :stroke-width="strokeWidth"></circle>
                <g>
                    <circle class="donut-segment"
                            :cx="cx" :cy="cy"
                            :r="radius"
                            fill="transparent"
                            :stroke="segmentColour"
                            :stroke-width="strokeWidth"
                            :stroke-dasharray="strokeDashArray"
                            stroke-dashoffset="25"
                            :class="animate"
                            aria-labelledby="Segment title"
                            role="presentation"
                            pointer-events="none">
                    </circle>
                    <title>{{dataVal}}%</title>
                </g>
                <text x='50%' y='50%' dy=".375em" >{{dataVal}}</text>

            </svg>

        </figure>
            <div class="dataTitle">{{dataTitle}}</div>
        </span>

</template>

<script>
/*
    TODO
    1. if cx or cy become adjustable then so too must viewBox values to compensate

    * */
export default {
  props: {
    dataVal: {
      default: 31
    },
    dataTitle: {
      default: "Data Title"
    },
    animation: {
      default: true
    },
    strokeWidth: {
      default: 7
    },
    segmentColour: {
      default: "#438dbc"
    },
    ringColour: {
      default: "#d2d3d4"
    },
    dataMinValue: {
      default: 0
    },
    dataMaxValue: {
      default: 100
    }
  },
  data() {
    return {
      radius: 15.91549430918954, // gives us a circumference of 100 for easy percentage rendering
      cx: 21,
      cy: 21
    };
  },
  computed: {
    strokeDashOffset() {
      return Math.round(
        this.circumference -
          (this.calculatedPercentage * this.circumference) / 100
      );
    },
    animate() {
      return this.animation ? "animate" : "";
    },
    strokeDashArray() {
      return (
        this.calculatedPercentage + " " + (100 - this.calculatedPercentage)
      );
      //return 100 * (this.dataVal - this.dataMinValue) / (this.dataMaxValue - this.dataMinValue) + " " + (100-this.dataVal);
    },
    mapBetween(currentNum, minAllowed, maxAllowed, min, max) {
      return (
        ((maxAllowed - minAllowed) * (currentNum - min)) / (max - min) +
        minAllowed
      );
    },
    calculatedPercentage() {
      return (
        (100 * (this.dataVal - this.dataMinValue)) /
        (this.dataMaxValue - this.dataMinValue)
      );
    }
  },
  methods: {}
};
</script>
<style scoped="true">
svg {
  height: 100%;
  pointer-events: none;
  position: relative;
  width: 100%;
}
svg text {
  fill: #438dbc;
  font-weight: bold;
  font-size: 0.75em;
  text-anchor: middle;
}
.dataTitle {
  text-align: center;
  color: #666;
  width: 100%;
  white-space: initial;
}

.donut-segment {
  stroke-dashoffset: 25;
}
.animate {
  animation: dash 1.5s ease-in-out forwards;
}
@keyframes dash {
  from {
    stroke-dasharray: 0, 100;
    stroke-dashoffset: 25;
  }
  to {
    stroke-dashoffset: 25;
  }
}
</style>
