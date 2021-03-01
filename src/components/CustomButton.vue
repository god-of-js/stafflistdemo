<template>
  <button
    id="btn"
    :class="[inactive ? 'btn-disabled ' : '']"
    :disabled="inactive"
    v-on="$listeners"
  >
      <slot />
  </button>
</template>

<script>
export default {
  name: "DefaultButton",
  props: {
    inactive: {
      type: Boolean,
      default: false
    },
    loading: {
      type: Boolean,
      default: false
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/styles/colors.scss";

#btn {
  width: 100%;
  padding: 10px;
  height: 56px;
  outline: none;
  background: $green;
  color: $white;
  box-sizing: border-box;
  border-radius: 4px;
  border: transparent;
  font-size: 0.9em;
  cursor: pointer;
  &:active {
    transform: scale(1.04, 1.03);
  }
}
.btn-disabled {
  opacity: 0.6;
  cursor: not-allowed;
}
</style>
