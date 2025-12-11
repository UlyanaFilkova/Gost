<template>
  <div class="product-page">
    <div class="gallery">
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
        <img :src="item.src" class="carousel-img" />
      </UCarousel>

      <div class="flex gap-1 justify-between pt-4 max-w-xs mx-auto">
        <div
            v-for="(item, index) in items"
            :key="index"
            class="size-11 opacity-25 hover:opacity-100 transition-opacity"
            :class="{ 'opacity-100': activeIndex === index }"
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

    <div class="info">
      <h1 class="title">{{ product.name }}</h1>

      <div class="brand">{{ product.brand }}</div>

      <div class="rating" v-if="product.rating">
        ⭐ {{ product.rating }}/{{ product.max_rating }}
      </div>

      <div class="price">{{ product.price.full }}</div>

      <div class="availability"
           :class="{ in_stock: product.availability_status === 'in_stock' }">
        {{ product.availability }}
      </div>

      <UIButton variant="primary" size="lg" block>
        В корзину
      </UIButton>
    </div>

    <div class="section">
      <h2>Характеристики</h2>
      <table class="features">
        <tbody>
        <tr v-for="f in product.features" :key="f.name">
          <td class="f-name">{{ f.name }}</td>
          <td class="f-value">{{ f.value }}</td>
        </tr>
        </tbody>
      </table>
    </div>

    <div class="section">
      <h2>Описание</h2>
      <p class="description" v-html="product.description" />
    </div>

  </div>
</template>

<script setup lang="ts">
import { productMock } from '~/data/mocks/products'
import type { ProductData } from '~/types/product'

const product: ProductData = productMock

const items = product.images


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
.product-page {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  padding: 20px 0;
}

@media (max-width: 900px) {
  .product-page {
    grid-template-columns: 1fr;
  }
}

.gallery {
  width: 100%;
}

.carousel {
  border-radius: 12px;
}

.carousel-img {
  width: 100%;
  height: auto;
  display: block;
}

.info {
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.title {
  font-size: 28px;
  font-weight: bold;
  color: var(--color-primary);
}

.brand {
  font-size: 16px;
  color: var(--color-gray-dark);
}

.rating {
  font-size: 16px;
  color: #f2b01e;
}

.price {
  font-size: 26px;
  font-weight: 700;
  color: var(--color-accent);
}

.availability {
  font-size: 15px;
  color: var(--color-gray-dark);
}
.availability.in_stock {
  color: #28a745;
  font-weight: 600;
}

.section {
  grid-column: 1 / -1;
  margin-top: 40px;
}

.section h2 {
  font-size: 22px;
  margin-bottom: 16px;
  font-weight: 600;
}

.features {
  width: 100%;
  border-collapse: collapse;
  background: var(--color-bg-light);
  border-radius: 12px;
  overflow: hidden;
}

.features tr:nth-child(even) {
  background: rgba(0,0,0,0.03);
}

.features td {
  padding: 10px 14px;
  font-size: 15px;
}

.f-name {
  width: 40%;
  font-weight: 600;
  color: var(--color-gray-dark);
}

.f-value {
  color: var(--color-primary);
}

.description {
  font-size: 15px;
  line-height: 1.6;
  color: var(--color-gray-dark);
}
</style>
