<template>
  <fieldset :class="[err ? 'error' : '', 'input-container']">
    <component :is="img" class="margin" />
    <input
      :type="type"
      :placeholder="placeholder"
      v-model="value"
      @input="$emit('data', value)"
      v-if="elementType === 'input'"
    />

    <select name="" id="" v-model="value" v-else @change="$emit('data', value)">
      <option
        v-for="(option, index) in optionsArr"
        :key="index"
        :value="option.value"
      >
        {{ option.text }}
      </option>
    </select>
  </fieldset>
</template>

<script>
import SelectImg from "./img/SelectImg";
import DateImg from "./img/DateImg";
import EmailImg from "./img/EmailImg";
export default {
  name: "CustomInputContainer",
  props: {
    err: {
      type: Boolean,
      default: false
    },
    type: {
      type: String,
      default: "text"
    },
    img: {
      type: String,
      default: ""
    },
    placeholder: {
      type: String
    },
    elementType: {
      type: String,
      default: "input"
    },
    optionsArr: {
      type: Array
    }
  },
  data: () => {
    return {
      value: ""
    };
  },
  components: {
    SelectImg,
    DateImg,
    EmailImg
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
