<template>
  <main class="home">
    <section class="sl-logo-container">
      <logo-img />
    </section>
    <section class="content-container">
      <article class="content">
        <h2>Level Up. Go Stafflist.</h2>
        <p>
          An administration & collaboration tool - Stafflist is the intersecting
          point of all the stakeholders in the staffing process.
        </p>
        <button @click="openModal" class="action">
          <img :src="menuIcon" alt="click button" width="10" />
          <span>Just Click me</span>
        </button>
      </article>
    </section>
    <modal v-if="modalStatus" />
  </main>
</template>

<script>
import IconBar from "@/assets/img/icon-bar.svg";
import Modal from "@/components/Modal.vue";
import LogoImg from "../components/img/LogoImg.vue";
export default {
  name: "Home",
  data: () => {
    return {
      menuIcon: IconBar,
      modal: false
    };
  },
  computed: {
    modalStatus() {
      return this.$store.state.modal;
    }
  },
  components: {
    Modal,
    LogoImg
  },
  methods: {
    openModal() {
      this.$store.commit("modalState", true);
    }
  }
};
</script>
<style lang="scss" scoped>
@import "../assets/styles/colors.scss";
@import "../assets/styles/sizes.scss";
.home {
  display: flex;
  justify-content: center;
  height: 100vh;
  padding-top: 3%;
  .sl-logo-container {
    padding-top: 5%;
    width: fit-content;
  }
  .content-container {
    width: 50%;
    display: flex;
    justify-content: flex-end;
    height: 90%;
    background-image: url("../assets/img/fig-1.svg"),
      url("../assets/img/fig-2.svg");
    background-repeat: no-repeat;
    background-size: 90% 65%, 65% 65%;
    background-origin: content-box;
    background-position: left bottom, right top;
    .content {
      width: 50%;
      margin-top: 5%;
      height: 200px;
      background-size: cover;
      background-image: url("../assets/img/fig-3.svg");
      border-radius: 12px;
      padding: 20px;
      padding-top: 18%;
      p {
        font-size: 1em;
        text-align: left;
        padding: 0;
      }
      button {
        background: $white;
        padding: 10px;
        outline: none;
        width: 125px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        height: 45px;
        border-radius: 5px;
        border: 1px solid $dark-color;
        cursor: pointer;
        float: right;
      }
    }
  }
}
h2 {
  padding: 0;
  margin: 0;
  text-align: left;
}
@media screen and (max-width: $mobile-break-point) {
  svg {
    #test-00 {
      fill: $white;
    }
  }
  .home {
    flex-direction: column;
    background-image: url("../assets/img/fig-2.svg");
    background-size: 100% 80%;
    background-repeat: no-repeat;
    background-position: top center;
    .sl-logo-container {
      width: 100%;
    }
    .content-container {
      width: 100%;
      height: 100%;
      background-image: url("../assets/img/fig-1.svg");
      background-size: 60% 70%;
      background-position: left bottom;
      .content {
        width: 85%;
        margin-top: -5%;
        height: 300px;
        background-size: cover !important;
        padding-top: 28%;
        clip-path: polygon(0 28%, 100% 0, 100% 100%, 0 70%);
        background: $white;
        .action {
          margin: auto;
          float: none;
        }
      }
    }
  }
}
</style>
