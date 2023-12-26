<template>
  <div class="calculator-wrapper">
    <div class="inputs">
      <div
        v-for="inputValue in inputValues"
        class="date-input"
        :class="{ error: inputValue.error }"
      >
        <label :for="`input-${inputValue.key}`">
          {{ inputValue.key === "date" ? "day" : inputValue.key }}
        </label>
        <input
          v-model="inputValue.value"
          type="text"
          :maxlength="inputValue.key === 'year' ? 4 : 2"
          :placeholder="inputValue.placeholder"
        />
        <span class="description">
          {{ isIncorrect(inputValue.key) ? inputValue.error : "" }}
        </span>
      </div>
    </div>
    <div class="separator">
      <div class="line"></div>
      <button class="icon-container" @click="checkValues">
        <IconArrow class="icon-arrow" />
      </button>
    </div>
    <div class="results-wrapper">
      <div class="result" v-for="result in resultValues">
        <span class="value">{{
          !!result.value || result.value === 0 ? result.value : "--"
        }}</span>
        <span class="title">{{ result.title }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import IconArrow from "./components/IconArrow.vue";
import dayjs from "dayjs";
import "dayjs/locale/fr";
dayjs.locale("fr");

const inputValues = ref([
  {
    key: "date",
    placeholder: "DD",
    value: "",
    description: "Must be a valid day",
    error: false,
  },
  {
    key: "month",
    placeholder: "MM",
    value: "",
    description: "Must be a valid month",
    error: false,
  },
  {
    key: "year",
    placeholder: "YYYY",
    value: "",
    description: "Must be in the past",
    error: false,
  },
]);

const resultValues = ref([
  { key: "year", title: "years", value: null },
  { key: "month", title: "months", value: null },
  { key: "date", title: "days", value: null },
]);

const isIncorrect = (key) => {
  const input = inputValues.value.find((input) => input.key === key);
  switch (input.key) {
    case "date":
      if (parseInt(input.value) > 31) return true;
      break;
    case "month":
      if (parseInt(input.value) > 12) return true;
      break;
    case "year":
      if (parseInt(input.value) > dayjs().year()) return true;
      break;
  }
};

const checkValues = () => {
  for (const input of inputValues.value) {
    if (isIncorrect(input.key)) return;
    if (input.value === "") return;
  }
  for (const result of resultValues.value) {
    const input = inputValues.value.find((input) => input.key === result.key);
    const newDate = dayjs().set(input.key, parseInt(input.value));
    const diff = newDate.diff(
      dayjs(),
      result.key === "date" ? "day" : result.key
    );
    result.value = Math.abs(diff);
  }
};
</script>

<style lang="scss">
@import "./assets/fonts/fonts.scss";

* {
  margin: 0;
  padding: 0;
  left: 0;
  top: 0;
}

:root {
  --white: hsl(0, 0%, 100%);
  --off-white: hsl(0, 0%, 94%);
  --light-grey: hsl(0, 0%, 86%);
  --smockey-grey: hsl(0, 1%, 44%);
  --off-black: hsl(0, 0%, 8%);
  --purple: hsl(259, 100%, 65%);
  --light-red: hsl(0, 100%, 67%);
}

#app {
  width: 100vw;
  height: 100vh;
  background: var(--off-white);
  @media (max-width: 375px) {
    padding: 1rem;
  }
}

.calculator-wrapper {
  box-sizing: border-box;
  padding: 1.25rem;
  display: flex;
  flex-direction: column;
  background-color: var(--white);
  border-radius: 1.25rem 1.25rem 5rem 1.25rem;
  transform: translateY(25%);
  .inputs {
    box-sizing: border-box;
    display: flex;
    gap: 1rem;
    width: 100%;
    .date-input {
      display: flex;
      flex-direction: column;
      gap: 0.325rem;
      label {
        font-family: "Poppins-Bold", sans-serif;
        color: var(--smockey-grey);
        font-size: 0.625rem;
        text-transform: uppercase;
        letter-spacing: 0.12rem;
      }
      input {
        box-sizing: border-box;
        width: 100%;
        font-family: "Poppins-Bold", sans-serif;
        font-size: 1.125rem;
        line-height: normal;
        padding: 0.75rem 0.5rem;
        border: 1px solid var(--light-grey);
        outline: none;
        border-radius: 0.5rem;
        color: var(--off-black);
        text-align: start;
        &::placeholder {
          color: var(--light-grey);
        }
      }
      .description {
        font-family: "Poppins-Italic", sans-serif;
        font-size: 0.5rem;
        height: 0.5rem;
        color: var(--light-red);
      }
    }
    .error {
      label {
        color: var(--light-red);
      }
      input {
        border-color: var(--light-red);
      }
    }
  }
  .separator {
    width: 100%;
    height: 6rem;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    .line {
      width: 100%;
      height: 0.06rem;
      background: var(--light-grey);
    }
    .icon-container {
      box-sizing: border-box;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      border-radius: 50%;
      background-color: var(--purple);
      border: none;
      padding: 0.75rem;
      .icon-arrow {
        width: 1.5rem;
        height: auto;
      }
    }
  }
  .results-wrapper {
    font-family: "Poppins-ExtraBoldItalic";
    font-size: 2.5rem;
    padding: 0.75rem 0;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;
    gap: 0.5rem;
    .result {
      display: flex;
      gap: 0.5rem;
      .value {
        color: var(--purple);
      }
    }
  }
}
</style>
