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
        <MostPopularCities />
        <PageFooter />
      </div>
    </div>

    <div class="page-right">
      <ServicesPage :city="city" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.page {
  display: flex;
  justify-content: center;
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
}
</style>
