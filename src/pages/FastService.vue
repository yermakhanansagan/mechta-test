<script lang="ts" setup>
import PageHeader from "../components/PageHeader.vue";
import CitySelectBlock from "../components/CitySelectBlock.vue";
import MostPopularCities from "../components/MostPopularCities.vue";
import PageFooter from "../components/PageFooter.vue";
import ServicesPage from "../components/ServiceSelector.vue";

import { ref } from "vue";

const city = ref("");
</script>

<template>
  <div class="page">
    <div class="page-left">
      <div class="page-left__container">
        <PageHeader />
        <CitySelectBlock @selected="(cityValue: string) => city = cityValue" />
        <MostPopularCities :class="{ hide: city }" />
        <PageFooter class="hide" />
      </div>
    </div>

    <div class="page-right">
      <ServicesPage :city="city" />
    </div>
    <PageFooter class="page-footer" />
  </div>
</template>

<style lang="scss" scoped>
.page {
  display: flex;
  height: 100%;
  &-left {
    padding: 20px 0;
    flex: 1;
    display: flex;
    justify-content: center;
    &__container {
      display: flex;
      flex-direction: column;
      gap: 5rem;
    }
  }
  &-right {
    flex: 1;
    background: #f7f7f7;
    border-radius: 2.5rem 0 0 2.5rem;
  }
  &-footer {
    display: none;
  }
}

@media (max-width: 768px) {
  .page {
    display: flex;
    flex-direction: column;
    gap: 1.875rem;

    &-left {
      padding: 1.2rem 1.563rem;
      flex: auto;
    }

    &-right {
      flex: auto;
      border-radius: 2.5rem 2.5rem 0 0;
      padding: 1.563rem;
      height: auto;
    }
    &-footer {
      display: flex;
      flex-direction: column-reverse;
      gap: 1.2rem;
      align-items: start;
      padding: 0 1.563rem 1.563rem;
    }
  }
  .hide {
    display: none;
  }
}
</style>
