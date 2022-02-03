<template>
  <div>
    <HelloWorld
      v-bind:inputValue="inputValue"
      v-on:updateText="updateRaza($event)"
    >
    </HelloWorld>

    <svg class="drawingBoard" width="75vw" height="75vh">
      <p id="drawingBroadId"></p>
      <rect
        @click="test"
        x="0"
        y="0"
        width="100%"
        height="100%"
        style="fill: rgb(255, 255, 253); stroke-width: 3; stroke: rgb(0, 0, 0)"
      />
      <svg height="100%" width="100%" xmlns="http://www.w3.org/2000/svg">
        <circle
          id="circle"
          cx="0"
          cy="0"
          r="5"
          stroke="black"
          stroke-width="1"
          fill="red"
        />
      </svg>
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
      cx: 0,
      cy: 0,
      inputValue: 0,
    };
  },
  // mounted() {
  //   this.test();
  // },
  // computed: {},
  methods: {
    logKey(e) {
      let screenLog = document.querySelector("#drawingBroadId");
      console.log(screenLog);
      // console.log(e.clientX);
      // console.log(e.clientY);
      // screenLog.innerText = `
      // Screen X/Y : ${e.screenX}, ${e.screenY}
      // Client X/Y : ${e.clientX}, ${e.clientY}
      // `;
      this.cx = e.clientX - window.innerWidth * 0.125;
      this.cy = e.clientY - window.innerHeight * 0.125;
      console.log(this.cx, this.cy);
      let svg = document.getElementById("circle");
      // let NS = svg.getAttribute("xmlns");
      // console.log(NS);
      svg.setAttribute("cx", this.cx);
      svg.setAttribute("cy", this.cy);
      // svg.setAttribute("r", this.inputValue);
      console.log(this.inputValue);
    },
    test(event) {
      this.logKey(event);
    },
    updateRaza(event) {
      this.inputValue = event;
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
</style>
