<template>
  <div>
    <button @click.prevent="clickFile" class="add-document-button">
      <plus-img />
      <span>Add document</span>
    </button>
    <span v-text="fileName" />
    <input type="file" class="file" @change="getFile" />
  </div>
</template>

<script>
import pickFileMixin from "@/mixins/pickFile.js";
import PlusImg from "./img/PlusImg";
export default {
  mixins: [pickFileMixin],
  data() {
    return {
      fileName: ""
    };
  },
  components: {
    PlusImg
  },
  methods: {
    // this method is being activated from the mixin pickFileMixin.
    handleDocument(file) {
      console.log(file);
      this.fileName = file.name;
      this.$emit("sendFile", file);
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/styles/colors.scss";
.add-document-button {
  outline: none;
  border: 2px solid $border-color;
  background: transparent;
  border-radius: 4px;
  padding: 6px;
  width: 150px;
  display: flex;
  justify-content: space-between;
  margin-top: 15px;
}
input[type="file"] {
  display: none;
}
div {
  display: flex;
  align-items: center;
}
</style>
