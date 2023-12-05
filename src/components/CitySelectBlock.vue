<script lang="ts" setup>
import CitySelect from "../components/CitySelect.vue";

defineEmits<{ (e: "selected", city: string): void }>();
</script>

<template>
  <div class="select-block">
    <div class="select-block__texts">
      <span class="select-block__texts-title">Delivery cost</span>
      <span class="select-block__texts-description">
        Enter name of the city to count delivery cost
      </span>
    </div>
    <CitySelect @selected="(city: string) => $emit('selected', city)" />
  </div>
</template>

<style lang="scss" scoped>
.select-block {
  display: flex;
  flex-direction: column;
  gap: 5rem;
  &__texts {
    display: flex;
    flex-direction: column;
    gap: 0.938rem;
    &-title {
      font-size: 3rem;
      font-weight: 700;
    }
    &-description {
      color: rgba(40, 48, 68, 0.5);
      font-size: 1.5rem;
    }
  }
}
</style>
