<template>
  <main class="form-card">
    <header class="form-card-heading">
      <span>Add Vacancy</span>
      <custom-button :setClass="'close-btn'" @click="closeModal">
        <close-button-img />
      </custom-button>
    </header>
    <form @submit.prevent="submit">
      <custom-input
        class="mt"
        :img="'SelectImg'"
        :elementType="'select'"
        :optionsArr="arr"
        @data="e => (data.project = e)"
      />
      <custom-input
        class="mt date"
        :img="'DateImg'"
        :type="'date'"
        @data="e => (data.date = e)"
      />
      <custom-input
        class="mt"
        :err="emailIsWrong"
        :img="'EmailImg'"
        :placeholder="'Email Address'"
        @data="e => (data.email = e)"
      />
      <fieldset class="checkbox-container mt">
        <legend class="text">Clearance for</legend>
        <div class="checkbox-outer">
          <input
            type="checkbox"
            name="clearance"
            v-model="data.clearanceForAll"
          />
          <label for="clearance">All</label>
        </div>
      </fieldset>
      <custom-button
        @click.prevent="additionalInformation = !additionalInformation"
        :setClass="'text'"
        class="additional-information"
      >
        <plus-img v-if="!additionalInformation" />
        <span v-else class="dash">-</span>
        <span>Additional Information</span>
      </custom-button>
      <div v-if="additionalInformation">
        <textarea
          name=""
          id=""
          cols="30"
          rows="10"
          placeholder="Additional staff information"
          v-model="data.additionalInformation"
        ></textarea>
        <add-document @sendFile="acceptFile" />
      </div>
      <custom-button class="mt" :inactive="emailCheck">SAVE</custom-button>
    </form>
  </main>
</template>

<script>
import axios from "axios";
import emailValidation from "@/helpers/emailValidation";
import CustomInput from "./CustomInput.vue";
import CustomButton from "./CustomButton.vue";
import AddDocument from "@/components/AddDocument";
import PlusImg from "./img/PlusImg";
import CloseButtonImg from "./img/CloseButtonImg";

export default {
  data: () => {
    return {
      arr: [
        {
          value: "Emergency hospital",
          text: "Emergency Hospital"
        }
      ],
      data: {
        email: null,
        file: null,
        project: null,
        clearanceForAll: null,
        date: null,
        additionalInformation: null
      },
      additionalInformation: false,
      emailIsWrong: false
    };
  },
  components: {
    CustomInput,
    CustomButton,
    AddDocument,
    PlusImg,
    CloseButtonImg
  },
  computed: {
    emailCheck() {
      return !emailValidation.email.test(this.data.email);
    }
  },
  methods: {
    submit() {
      console.log(this.data);
      if (!emailValidation.email.test(this.data.email)) {
        this.emailIsWrong = true;
        return;
      }
      axios.post("https://someurl/post-request", this.data).then(() => {});
    },
    closeModal() {
      this.$store.commit("modalState", false);
    },
    acceptFile(file) {
      this.data.file = file;
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/styles/colors.scss";
@import "../assets/styles/sizes.scss";
.form-card {
  background: $white;
  width: 30%;
  padding-top: 1%;
  padding-bottom: 2%;
  overflow-y: auto;
  max-height: 70%;
  &-heading {
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid $border-color;
    padding: 7px;
    span {
      font-weight: bold;
    }
    button {
      background: transparent;
      outline: none;
      border: none;
      cursor: pointer;
      border-radius: 50%;
      height: 25px;
    }
  }
  form {
    padding: 15px;
  }
}
.mt {
  margin-top: 15px;
}
#err {
  &::placeholder {
    color: red;
  }
}
.date {
  width: 50%;
}
legend {
  margin-left: 0px;
  text-align: left;
  font-size: 0.9em;
}
.checkbox-container {
  border: 1px solid $border-color;
  height: 56px;
  width: 100%;
  background: $white;
  box-sizing: border-box;
  .checkbox-outer {
    display: flex;
    align-items: center;
    font-size: 0.9em;
  }
  input[type="checkbox"] {
    width: initial;
    margin-right: 10px;
  }
}
textarea {
  outline: none;
  border: 1px solid $border-color;
  width: 90%;
  margin-top: 15px;
  padding: 15px;
}
.dash {
  font-size: 24px;
}
@media screen and (max-width: $mobile-break-point) {
  .form-card {
    background: $white;
    width: 100%;
    height: 100%;
    max-height: 100%;
  }
}
</style>
