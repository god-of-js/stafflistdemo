<template>
  <fieldset :class="[err ? 'error' : '', 'input-container']">
    <slot name="icon" class="icon"></slot>
    <div class="margin"></div>
    <slot name="input"></slot>
  </fieldset>
</template>

<script>
export default {
  name: "CustomInputContainer",
  props: {
    err: {
      type: Boolean,
      default: false
    }
  }
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/colors.scss";
.input-container {
  width: 100%;
  background: $white;
  line-height: 1.2em;
  height: 56px;
  padding: 7px;
  border-radius: 5px;
  border: 1px solid $border-color;
  font-size: 1em;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  input {
    outline: none;
    border: transparent;
    width: 100%;
    background-color: $white;
    margin-left: 15px;
    ::placeholder {
      color: $border-color;
    }
  }
  select {
    width: 95%;
    height: 100%;
    outline: none;
    border: transparent;
    background: $white;
  }
}
.error {
  border-color: red;
}
input[type="date"]::-webkit-inner-spin-button,
input[type="date"]::-webkit-calendar-picker-indicator {
  display: none;
  -webkit-appearance: none;
}
.margin {
  margin-right: 15px;
}
</style>
