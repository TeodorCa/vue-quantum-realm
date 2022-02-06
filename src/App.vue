<template>
  <div>
    <RadiusSetter v-on:updateText="updateRadius($event)"> </RadiusSetter>

    <svg id="drawingBox" class="box" ref="box" width="75vw" height="75vh">
      <rect
        @click="addCircleToList"
        x="0"
        y="0"
        width="100%"
        height="100%"
        style="fill: rgb(255, 255, 240); stroke-width: 3; stroke: rgb(0, 0, 0)"
      />
      <svg v-for="circle in circleList" :key="circle.id">
        <svg width="20" height="20">
          <circle
            :id="circle.id"
            :cx="circle.cx"
            :cy="circle.cy"
            :r="circle.r"
            fill="red"
            stroke="black"
            stroke-width="1"
            @mousedown="drag"
            @mouseup="drop"
          ></circle>
        </svg>
      </svg>
    </svg>
  </div>
</template>
<script>
import RadiusSetter from "./components/RadiusSetter.vue";
import { v4 as uuid } from "uuid";
export default {
  components: {
    RadiusSetter,
  },
  data: function () {
    return {
      inputValue: this.inputValue,
      circleList: [],
    };
  },
  methods: {
    addCircleToList(eventDetails) {
      const cx = eventDetails.clientX - window.innerWidth * 0.125;
      const cy = eventDetails.clientY - window.innerHeight * 0.125;
      const newCircle = {
        id: uuid(),
        cx: cx,
        cy: cy,
        r: this.inputValue,
      };
      this.circleList = [...this.circleList, newCircle];
    },
    updateRadius: function (event) {
      this.inputValue = event;
    },
    drag() {
      this.$refs.box.addEventListener("mousemove", this.move);
    },
    drop() {
      this.$refs.box.removeEventListener("mousemove", this.move);
    },
    move(event) {
      const circleId = event.target.id;
      const cx = event.offsetX;
      const cy = event.offsetY;
      const newCircleList = this.circleList.map((circle) => {
        if (circle.id === circleId) {
          return {
            ...circle,
            cx: cx,
            cy: cy,
          };
        } else {
          return circle;
        }
      });
      this.circleList = newCircleList;
    },
  },
};
</script>

<style>
body {
  display: flex;
  justify-content: center;
  align-items: center;
}
.box {
  position: absolute;
  top: 12.5%;
  bottom: 12.5%;
  left: 12.5%;
  right: 12.5%;
  cursor: pointer;
}
svg {
  display: contents;
}
svg.box {
  display: block;
}
</style>
