<script lang="ts" setup>
const cities = [
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
</script>

<template>
  <div class="cities">
    <span class="cities__title">Most popular cities</span>
    <div class="cities__cities">
      <span
        class="cities__cities-city"
        v-for="(city, index) in cities"
        :key="index"
      >
        {{ city }}
      </span>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.cities {
  &__title {
    font-size: 1.5rem;
  }
  &__cities {
    margin-top: 2.625rem;
    display: grid;
    grid-auto-flow: column;
    grid-template-rows: repeat(5, 1fr);
    gap: 1rem;
    &-city {
      width: 224px;
      padding: 0 0 0.625rem 1.2rem;
      border-bottom: 1px solid #e9f0eb;
      color: #28304480;
      font-size: 1.2rem;
    }
  }
}
</style>
