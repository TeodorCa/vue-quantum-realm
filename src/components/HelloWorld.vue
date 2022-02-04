<template>
  <div>
    <div id="radiusSetter" class="radiusSetter">
      <label for="circleSize">Radius : </label>
      <input
        id="circleSize"
        type="number"
        placeholder="5"
        value="inputValue"
        @input="updateText"
      />
      <p>px</p>
    </div>
  </div>
</template>

<script>
export default {
  // props: ["inputValue"],
  // data: function () {
  //   return {
  //     newText: "",
  //   };
  // },
  methods: {
    updateText: function(value) {
      // this.newText = value.data;
      this.$emit('updateText', value.data)
      // let inputValue = this.newText;
      console.log(value.data);
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
