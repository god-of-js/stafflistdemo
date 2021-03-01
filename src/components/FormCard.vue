<template>
  <div class="form-card">
    <div class="form-card-heading">
      <span>Add Vacancy</span>
      <button class="close-btn" @click="closeModal">
        <svg
          width="10px"
          height="11px"
          viewBox="0 0 10 11"
          version="1.1"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
        >
          <title>icon-close</title>
          <g
            id="test"
            stroke="none"
            stroke-width="1"
            fill="none"
            fill-rule="evenodd"
          >
            <g
              id="test-02"
              transform="translate(-888.000000, -266.000000)"
              fill="#000000"
              fill-rule="nonzero"
            >
              <g id="vacancy">
                <path
                  d="M896.765013,276.310667 L897.373143,275.702537 C897.708931,275.366749 897.708931,274.822359 897.373143,274.486304 L894.636852,271.750013 L897.373143,269.013721 C897.708931,268.67796 897.708931,268.133543 897.373143,267.797488 L896.765013,267.189358 C896.429225,266.85357 895.884835,266.85357 895.54878,267.189358 L892.812489,269.925649 L890.076197,267.189358 C889.740436,266.85357 889.196019,266.85357 888.859964,267.189358 L888.251834,267.797488 C887.916046,268.133276 887.916046,268.677666 888.251834,269.013721 L890.988125,271.750013 L888.251834,274.486304 C887.916046,274.822065 887.916046,275.366482 888.251834,275.702537 L888.859964,276.310667 C889.195752,276.646455 889.740436,276.646455 890.076197,276.310667 L892.812489,273.574376 L895.54878,276.310667 C895.884541,276.646455 896.429225,276.646455 896.765013,276.310667 Z"
                  id="icon-close"
                ></path>
              </g>
            </g>
          </g>
        </svg>
      </button>
    </div>
    <form @submit.prevent="submit">
      <custom-input-container class="mt">
        <template v-slot:icon> <select-img /></template>
        <template v-slot:input>
          <select name="" id="" v-model="data.project">
            <option disabled selected hidden value="">Project</option>
            <option
              v-for="(option, index) in arr"
              :key="index"
              :value="option.value"
            >
              {{ option.text }}
            </option>
          </select></template
        >
      </custom-input-container>
      <div class="date-container">
        <custom-input-container class="mt">
          <template v-slot:icon> <date-img /></template>
          <template v-slot:input>
            <input type="date" v-model="data.date" />
          </template>
        </custom-input-container>
      </div>
      <custom-input-container class="mt" :err="emailIsWrong">
        <template v-slot:icon> <email-img :err="emailIsWrong"/></template>
        <template v-slot:input>
          <input
            type="email"
            v-model="data.email"
            placeholder="Email Address"
            :id="emailIsWrong ? 'err' : ''"
          />
        </template>
      </custom-input-container>
      <fieldset class="checkbox-container mt">
        <legend class="text">Clearance for</legend>
        <div class="checkbox-outer">
          <input
            type="checkbox"
            name="clearance"
            v-model="data.clearanceForAll"
          />
          <label for="clearance">All</label><br />
        </div>
      </fieldset>
      <div class="additional-information">
        <button
          type="text"
          @click.prevent="additionalInformation = !additionalInformation"
          class="text"
        >
          <plus-img v-if="!additionalInformation" />
          <span v-else class="dash">-</span>
          <span>Additional Information</span>
        </button>
      </div>
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
  </div>
</template>

<script>
import axios from "axios";
import emailValidation from "@/helpers/emailValidation";
import CustomInputContainer from "./CustomInputContainer.vue";
import CustomButton from "./CustomButton.vue";
import AddDocument from "@/components/AddDocument";
import PlusImg from "./img/PlusImg";
import SelectImg from "./img/SelectImg";
import DateImg from "./img/DateImg";
import EmailImg from "./img/EmailImg";

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
    CustomInputContainer,
    CustomButton,
    AddDocument,
    SelectImg,
    DateImg,
    EmailImg,
    PlusImg
  },
  computed: {
    emailCheck() {
      return !emailValidation.email.test(this.data.email);
    }
  },
  methods: {
    submit() {
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
.close-btn:hover {
  background-color: $dark-color;
  color: $white;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 25px;
  height: 25px;
  #test-02 {
    fill: $white;
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
.date-container {
  width: 50%;
}
.checkbox-container {
  border: 1px solid $border-color;
  height: 56px;
  width: 100%;
  background: $white;
  box-sizing: border-box;
  .text {
    margin-left: 0px;
    text-align: left;
    font-size: 0.9em;
  }
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
.additional-information {
  padding-top: 15px;
  display: flex;
  .text {
    font-size: 0.9em;
    background: transparent;
    border: transparent;
    outline: none;
    cursor: pointer;
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
