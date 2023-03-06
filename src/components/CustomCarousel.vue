<template>
  <div class="flex justify-between pb-5 ml-8 mr-6">
    <RouterLink
      to="/artist"
      @mouseenter="isHoverCategory = true"
      @mouseleave="isHoverCategory = false"
      :class="isHoverCategory ? 'hover:text-[#EF5456]' : 'text-white'"
      class="flex items-center font-semibold text-xl cursor-pointer"
    >
      {{ category }}
      <ChevronRight
        :fillColor="isHoverCategory ? '#EF5465' : '#FFFFFF'"
        :size="25"
        class="mt-1"
      />
    </RouterLink>
    <div class="flex items-center">
      <button class="rounded-full p-2 hover:bg-[#2b2b2b]" @click="slideTo(false)">
        <ChevronLeft fillColor="#FFFFFF" :size="30" />
      </button>
      <div class="px-2"></div>
      <button class="rounded-full p-2 hover:bg-[#2b2b2b]" @click="slideTo(true)">
        <ChevronRight fillColor="#FFFFFF" :size="30" />
      </button>
    </div>
  </div>
  <carousel
    class="mr-8"
    v-model="currentSlide"
    :items-to-show="4"
    :transition="800"
    snapAlign="start"
  >
    <slide class="flex items-baseline" v-for="slide in data" :key="slide">
      <SliderItem :slide="slide" />
    </slide>
  </carousel>
</template>

<script setup>
import { toRefs, ref } from "vue";
import { RouterLink } from "vue-router";
//icon
import ChevronLeft from "vue-material-design-icons/ChevronLeft.vue";
import ChevronRight from "vue-material-design-icons/ChevronRight.vue";
import SliderItem from "./SliderItem.vue";
import "vue3-carousel/dist/carousel.css";
import { Carousel, Slide } from "vue3-carousel";

let currentSlide = ref(0);
let isHoverCategory = ref(false);

const props = defineProps({
  category: String,
  data: Array,
});

const { data, category } = toRefs(props);

const slideTo = (val) => {
  if (val && currentSlide.value <= 7) {
    let res = currentSlide.value + 4;
    if (res <= 12) {
      currentSlide.value = currentSlide.value + 4;
    } else if (res > 12) {
      currentSlide.value = 12;
    }
  } else if (!val) {
    let res = currentSlide.value - 4;
    if (res > 0) {
      currentSlide.value = currentSlide.value - 4;
    } else if (res < 1) {
      currentSlide.value = 0;
    }
  }
};
</script>
