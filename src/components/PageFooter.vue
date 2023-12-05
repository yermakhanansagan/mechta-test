<script lang="ts" setup>
import Visa from "../assets/cardServices/visa.svg";
import Mastercard from "../assets/cardServices/mastercard.svg";
import Maestro from "../assets/cardServices/maestro.svg";
import Processing from "../assets/cardServices/processing.svg";

const cardServices = [
  { name: "visa", img: Visa },
  { name: "mastercard", img: Mastercard },
  { name: "maestro", img: Maestro },
  { name: "processing", img: Processing },
];
</script>

<template>
  <div class="footer">
    <div class="footer__rights">
      <span>All rights reserved</span>
      <span> Fast service 2021</span>
    </div>
    <div class="footer__services">
      <img
        :alt="`${cardService.name} logo`"
        :src="cardService.img"
        v-for="(cardService, index) in cardServices"
        :key="index"
        height="14"
      />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  &__rights {
    display: flex;
    flex-direction: column;
    font-size: 0.875rem;
    color: #28304480;
  }
  &__services {
    display: flex;
    gap: 0.625rem;
  }
}
</style>
