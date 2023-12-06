<script lang="ts" setup>
defineProps<{
  type: string;
  price: number;
  img: string;
  available: boolean;
  selected: boolean;
}>();

defineEmits<{ (e: "onSelect", type: string): void }>();
</script>

<template>
  <button
    class="service"
    :class="{ 'not-available': !available, selected: selected }"
    @click="$emit('onSelect', type)"
  >
    <div class="service__info-container">
      <div class="service__info">
        <span class="service__info__title">{{ type }}</span>
        <span class="service__info__cost">{{ price }}$</span>
      </div>
      <span class="service__img">
        <img :alt="`${type} image`" :src="img" />
      </span>
    </div>
    <div v-if="selected" class="service__accept">
      <img class="service__accept-icon" src="../assets/accept.svg" />
    </div>
  </button>
</template>

<style lang="scss" scoped>
.service {
  margin: 0;
  padding: 0;
  border: none;
  background: #fff;
  border-radius: 22px;
  display: flex;
  cursor: pointer;
  height: 224px;
  width: 523px;
  border: 1px solid #e9f0eb;
  &__info-container {
    display: flex;
    width: 100%;
    height: 100%;
    justify-content: space-between;
    padding: 2rem;
  }
  &__info {
    display: flex;
    flex-direction: column;
    height: 100%;
    text-align: start;
    justify-content: space-between;
    &__title {
      font-size: 2.25rem;
      font-weight: 700;
    }

    &__cost {
      color: #78a1bb;
      font-size: 3.125rem;
      font-weight: 700;
    }
  }
  &__img {
    height: 100%;
    display: flex;
    align-items: center;
  }
  &__accept {
    border-radius: 0 22px 22px 0;
    background: linear-gradient(
      310deg,
      #65b3e4 23.89%,
      rgba(255, 255, 255, 0) 81.27%
    );
    display: flex;
    align-items: center;
    justify-content: center;
    width: 6.5rem;
    height: 100%;
    svg {
      fill: #fff;
    }
  }
}

.not-available {
  background: transparent;
  pointer-events: none;
}
.selected {
  border: none;
}
@media (max-width: 768px) {
  .service {
    width: 271px;
    height: 172px;
    &__info-container {
      padding: 1.2rem;
    }
    &__info {
      display: flex;
      flex-direction: column;
      height: 100%;
      text-align: start;
      justify-content: space-between;
      &__title {
        font-size: 1.5rem;
        font-weight: 700;
      }

      &__cost {
        color: #78a1bb;
        font-size: 2rem;
        font-weight: 700;
      }
    }
    &__img {
      display: flex;
      align-items: center;
      img {
        height: 85px;
        width: 85px;
      }
    }
    &__accept {
      width: 2.625rem;
    }
  }
}
</style>
