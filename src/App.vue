<template>
  <div>
    <HelloWorld v-on:updateText="updateRaza($event)"> </HelloWorld>

    <svg id="drawingBox" class="drawingBoard" width="75vw" height="75vh">
      <rect
        @click="test"
        x="0"
        y="0"
        width="100%"
        height="100%"
        style="fill: rgb(255, 255, 240); stroke-width: 3; stroke: rgb(0, 0, 0)"
      />
      <!-- <svg height="100%" width="100%" xmlns="http://www.w3.org/2000/svg">
        <circle id="circle" stroke="black" stroke-width="1" fill="red" />
      </svg> -->
    </svg>
  </div>
</template>
<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  components: {
    HelloWorld,
  },
  data: function () {
    return {
      inputValue: 5,
      cx: 0,
      cy: 0,
    };
  },
  // mounted() {
  //   this.test();
  // },
  // computed: {},
  methods: {
    logKey(e) {
      this.cx = e.clientX - window.innerWidth * 0.125;
      this.cy = e.clientY - window.innerHeight * 0.125;
    },
    drawingCircle() {
      let svgCircle = document.createElementNS(
        "http://www.w3.org/2000/svg",
        "svg"
      );

      svgCircle.setAttribute("width", "20");
      svgCircle.setAttribute("height", "20");
      let cir1 = document.createElementNS(
        "http://www.w3.org/2000/svg",
        "circle"
      );
      console.log(this.cx, this.cy, this.inputValue);

      cir1.setAttribute("cx", this.cx);
      cir1.setAttribute("cy", this.cy);
      cir1.setAttribute("r", this.inputValue);
      cir1.setAttribute("fill", "red");
      cir1.setAttribute("stroke", "black");
      cir1.setAttribute("stroke-width", "1");

      svgCircle.appendChild(cir1);

      document.getElementById("drawingBox").appendChild(svgCircle);
    },
    updateRaza: function (event) {
      this.inputValue = event;
    },
    test(event) {
      this.logKey(event);
      this.drawingCircle();
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
.drawingBoard {
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
svg.drawingBoard {
  display: block;
}
</style>
