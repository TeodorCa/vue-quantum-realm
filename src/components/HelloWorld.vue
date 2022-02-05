<template>
  <div>
    <div id="radiusSetter" class="radiusSetter">
      <label for="circleSize">Radius : </label>
      <input
        id="circleSize"
        type="number"
        :placeholder="placeholderValue"
        :value="inputValue"
        @input="updateText"
        @focus="transformInputToValue"
      />
      <p>px</p>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      inputValue: "",
      placeholderValue: "",
    };
  },
  mounted() {
    this.placeholderValue = this.getRandomInputValue();
  },
  methods: {
    updateText: function (eventDetails) {
      // this.newText = value.data;
      this.$emit("updateText", eventDetails.target.value);
      this.inputValue = eventDetails.target.value;
      // let inputValue = this.newText;

      console.log(eventDetails.target.value);
    },
    getRandomInputValue: function () {
      let randomInputValue = Math.random() * 5 + 5;
      let randomInputValueTruncated = Math.round(randomInputValue);
      return randomInputValueTruncated;
    },
    transformInputToValue: function (eventDetails) {
      if (this.inputValue === "") {
        let placeholderValue = eventDetails.target.placeholder;
        this.$emit("updateText", placeholderValue);
        this.inputValue = placeholderValue;
        console.log(placeholderValue);
      }
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
