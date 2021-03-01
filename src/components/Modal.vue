<template>
  <div id="modal">
    <modal-wrap> <component :is="activeModal" /> </modal-wrap>
  </div>
</template>

<script>
import FormCard from "./FormCard.vue";
import ModalWrap from "./ModalWrap";
export default {
  name: "Modal",
  data: () => {
    return {
      activeModal: "FormCard",
    };
  },
  components: {
    FormCard,
    ModalWrap,
  },
};
</script>

<style lang="scss" scoped>
</style>
