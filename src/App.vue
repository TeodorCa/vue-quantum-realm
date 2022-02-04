<template>
  <div>
    <HelloWorld
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
        style="fill: rgb(255, 255, 240); stroke-width: 3; stroke: rgb(0, 0, 0)"
      />
      <svg height="100%" width="100%" xmlns="http://www.w3.org/2000/svg">
        <circle
          id="circle"

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
      inputValue: 5,
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
      let svg = document.getElementById("circle");
      let NS = svg.getAttribute("xmlns");
      let c = document.createElementNS(NS,'circle')
      
      this.cx = e.clientX - window.innerWidth * 0.125;
      this.cy = e.clientY - window.innerHeight * 0.125;
      
      c.setAttribute("cx", this.cx);
      c.setAttribute("cy", this.cy);
      c.setAttribute("r", this.inputValue);

      svg.appendChild(c);

      console.log(this.cx, this.cy);

      // console.log(NS);
      svg.setAttribute("cx", this.cx);
      svg.setAttribute("cy", this.cy);
      svg.setAttribute("r", this.inputValue);
      console.log(this.inputValue);
    },
    test(event) {
      this.logKey(event);
    },
    updateRaza: function(event) {
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
