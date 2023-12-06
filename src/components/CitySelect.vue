<script lang="ts" setup>
import { computed, ref, watch } from "vue";

const emit = defineEmits<{ (e: "selected", city: string): void }>();

const modelValue = ref("");
const selected = ref(false);
const error = ref(false);

const options = [
  "Nur - Sultan",
  "Almaty",
  "Shymkent",
  "Atyrau",
  "Aktau",
  "Zhana Turmis",
  "Karaganda",
  "Kentau",
  "Aitei",
  "Pavlodar",
];

function onSelect(option: string) {
  if (!options.includes(option)) {
    selected.value = true;
    error.value = true;
    return;
  }
  modelValue.value = option;
  selected.value = true;
  error.value = false;
  emit("selected", option);
}

function onCLose() {
  modelValue.value = "";
  selected.value = false;
  error.value = false;
  emit("selected", modelValue.value);
}

const open = computed(
  () => modelValue && filteredCities.value.length && !selected
);

const filteredCities = computed(() =>
  options.filter((option: string) =>
    option.toLowerCase().includes(modelValue.value.toLowerCase())
  )
);

watch(
  () => modelValue.value,
  (newValue: string) => {
    if (!newValue) {
      selected.value = false;
      emit("selected", modelValue.value);
    }
  }
);
</script>

<template>
  <div class="city-select" :class="{ open: open }">
    <div
      class="city-select__wrapper"
      :class="{
        'wrapper__on-open': open,
        error: error && !modelValue,
      }"
    >
      <input
        class="city-select__input"
        v-model="modelValue"
        placeholder="Enter name of the city"
      />
      <div class="city-select__buttons">
        <button
          v-if="!selected"
          class="city-select__button-select"
          @click="onSelect(modelValue)"
        >
          ENTER
        </button>
        <button
          v-else
          class="city-select__button-close"
          :class="{ 'button-error': error }"
          @click="onCLose"
        >
          X
        </button>
      </div>
    </div>
    <div
      v-if="modelValue && !selected"
      class="city-select__options"
      :class="{ 'options__on-open': open }"
    >
      <button
        v-for="city in filteredCities"
        :key="city"
        @click="onSelect(city)"
      >
        {{ city }}
      </button>
    </div>

    <span
      v-if="error && modelValue && selected"
      class="city-select__error-message"
    >
      We didn’t found such city. Please check spelling</span
    >
  </div>
</template>

<style lang="scss" scoped>
.city-select {
  display: flex;
  font-size: 1.5rem;
  flex-direction: column;
  min-width: 523px;
  width: fit-content;
  position: relative;
  &__wrapper {
    display: flex;
    border: 1px solid #e9f0eb;
    border-radius: 50px;
  }
  &__input {
    width: 100%;
    padding: 1.188rem 0 1rem 2.25rem;
    border-radius: 50px 0 0 50px;
    border: none;
    font-size: 1.5rem;
    font-weight: 700;
    outline: none;
    &::placeholder {
      color: #d9e4dc;
    }
  }
  &__button-select {
    padding: 1.188rem 3rem 1rem;
    border-radius: 50px;
    font-size: 1.5rem;
    background: linear-gradient(
      280deg,
      #65b3e4 15.15%,
      rgba(120, 161, 187, 0) 171.55%
    );
    border: none;
    font-weight: 700;
    color: #fff;
    cursor: pointer;
    &:hover {
      opacity: 0.7;
    }
  }
  &__button-close {
    height: 100%;
    width: 67px;
    border-radius: 50px;
    font-size: 1.5rem;
    background: linear-gradient(
      280deg,
      #65b3e4 15.15%,
      rgba(120, 161, 187, 0) 171.55%
    );
    border: none;
    font-weight: 700;
    color: #fff;
    cursor: pointer;
    &:hover {
      opacity: 0.7;
    }
  }
  &__options {
    padding: 0 1.5rem 0 1.125rem;
    position: absolute;
    width: 100%;
    display: flex;
    flex-direction: column;
    top: 100%;
    z-index: 999;
    background: white;
    min-height: auto;
    max-height: 300px;
    overflow-y: auto;
    button {
      background: none;
      border: none;
      outline: none;
      text-align: start;
      padding: 1.5rem 0 0.625rem 1.2rem;
      font-size: 1.2rem;
      border-bottom: 1px solid #e9f0eb;
      cursor: pointer;
      &:hover {
        opacity: 0.7;
      }
    }

    &:nth-last-child(n) {
      border-bottom: none;
    }
  }
  &__error-message {
    color: #ff4757;
    font-size: 1.2rem;
    margin-top: 1rem;
  }
}

.open {
  border-radius: 31px 31px 0 0;
  border: 1px solid #e9f0eb;
  background: #fff;
  box-shadow: 0px 0px 20px 0px rgba(120, 161, 187, 0.3);
}
.wrapper__on-open {
  border: none;
  border-radius: inherit;
}
.options__on-open {
  border-radius: 0 0 31px 31px;
}

.error {
  border-radius: 50px;
  border: 1px solid #ff4757;
}

.button-error {
  background: linear-gradient(
    280deg,
    #ff4757 15.15%,
    rgba(255, 255, 255, 0) 171.55%
  );
}

@media (max-width: 768px) {
  .city-select {
    min-width: 270px;

    &__input {
      padding: 1rem 0 0.9rem 1.2rem;
      font-size: 1rem;
    }
    &__button-select {
      padding: 1rem;
      font-size: 1rem;
    }
  }
}
</style>
