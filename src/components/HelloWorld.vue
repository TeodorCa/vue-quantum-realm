<template>
  <div>
    <div id="radiusSetter" class="radiusSetter">
      <label for="circleSize">Radius : </label>
      <input
        id="circleSize"
        type="number"
        placeholder="7"
        value="inputValue"
        @input="updateText"
      />
      <p>px</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["inputValue"],
  data: function () {
    return {
      newText: "",
    };
  },
  methods: {
    updateText(value) {
      this.newText = value.data;

      // let inputValue = this.newText;
      console.log(this.newText);
    },
  },
};
</script>

<style>
.radiusSetter {
  display: flex;
  align-items: center;
}
</style>
