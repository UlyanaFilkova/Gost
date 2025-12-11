<template>
  <div class="ui-carousel-gallery">
    <UCarousel
        ref="carousel"
        v-slot="{ item }"
        arrows
        :items="items"
        :prev="{ onClick: onClickPrev, color: 'primary' }"
        :next="{ onClick: onClickNext, variant: 'solid' }"
        class="carousel"
        @select="onSelect"
    >
      <img :src="item.src" :alt="item.alt" class="carousel-img" />
    </UCarousel>

    <div class="thumbs">
      <div
          v-for="(item, index) in items"
          :key="index"
          class="thumb"
          :class="{ active: activeIndex === index }"
          @click="select(index)"
      >
        <img :src="item.src"
             :alt="item.alt"
             width="44"
             height="44"
             class="rounded-lg"
        >
      </div>
    </div>

  </div>
</template>

<script setup lang="ts">
import type { PropType } from 'vue'

const props = defineProps({
  items: {
    type: Array as PropType<Array<{ src: string; alt?: string }>>,
    required: true
  }
})

const carousel = useTemplateRef('carousel')
const activeIndex = ref(0)

function onClickPrev() {
  activeIndex.value--
}
function onClickNext() {
  activeIndex.value++
}
function onSelect(index: number) {
  activeIndex.value = index
}

function select(index: number) {
  activeIndex.value = index

  carousel.value?.emblaApi?.scrollTo(index)
}
</script>

<style scoped>
.ui-carousel-gallery {
  width: 100%;
}

.carousel-img {
  width: 100%;
  display: block;
  border-radius: 12px;
}

.thumbs {
  display: flex;
  gap: 6px;
  justify-content: center;
  padding-top: 12px;
}

.thumb {
  width: 44px;
  height: 44px;
  opacity: 0.3;
  cursor: pointer;
  transition: 0.2s;
}

.thumb.active,
.thumb:hover {
  opacity: 1;
}

.thumb img {
  width: 100%;
  height: 100%;
  border-radius: 8px;
  object-fit: cover;
}
</style>
