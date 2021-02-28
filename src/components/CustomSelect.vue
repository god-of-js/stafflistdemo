<template>
  <div class="custom-select">
    <select name="" id="">
      <option disabled selected hidden>Project</option>
      <option v-for="(option, index) in arr" :key="index" :value="option.value">
        {{ option.text }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    arr: {
      type: Array,
      default: () => [
        {
          value: "Emergency hospital",
          text: "Emergency Hospital"
        }
      ]
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/styles/colors.scss";
.custom-select {
  border: 1px solid $border-color;
  display: flex;
  align-items: center;
  width: 100%;
  background: $white;
  line-height: 1.2em;
  height: 56px;
  padding: 7px;
  border-radius: 5px;
  outline: none;
  border: 1px solid $border-color;
  font-size: 1em;
  box-sizing: border-box;
  select {
    width: 95%;
    outline: none;
    border: transparent;
  }
}
svg {
  margin-right: 15px;
}
</style>
