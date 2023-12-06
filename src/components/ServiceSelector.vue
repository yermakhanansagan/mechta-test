<script lang="ts" setup>
import Pick from "../assets/services/pick.svg";
import Delivery from "../assets/services/delivery.svg";
import Post from "../assets/services/post.svg";

import axios from "axios";
import { defineAsyncComponent, ref, watch } from "vue";

const ServiceContainer = defineAsyncComponent(
  () => import("./ServiceContainer.vue")
);

type ServiceType = "pickup" | "courier" | "post";
type CityInfo = {
  city: string;
  type: string;
  available: boolean;
  price: number;
};

const props = defineProps<{ city: string }>();

const cityInfo = ref<CityInfo[]>([]);
const selected = ref<ServiceType | "">("");

function defineImage(type: ServiceType) {
  switch (type) {
    case "pickup":
      return Pick;
    case "courier":
      return Delivery;
    case "post":
      return Post;
  }
}

async function getData(city: string) {
  try {
    const response = await axios.get(
      "https://test-frontend.stage.mechta.market/delivery/check",
      {
        params: {
          search: city,
        },
      }
    );
    cityInfo.value = response.data as unknown as CityInfo[];
  } catch (error) {
    console.log(error);
  }
}

watch(
  () => props.city,
  async (newValue: string) => {
    if (newValue) {
      getData(newValue.toLowerCase());
    } else {
      cityInfo.value = [];
      selected.value = "";
    }
  }
);
</script>

<template>
  <div class="services">
    <ServiceContainer
      v-for="item in cityInfo"
      :key="item.type"
      :type="item.type"
      :price="item.price"
      :available="item.available"
      :img="defineImage(item.type as ServiceType)"
      :selected="selected === item.type"
      @on-select="(type) => (selected = type as ServiceType)"
    />
  </div>
</template>

<style lang="scss" scoped>
.services {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  gap: 1.125rem;
}
</style>
