<template>
  <div class="product-page">
    <UBreadcrumb :items="breadcrumbs" class="breadcrumb" />
    <div class="top-block">

      <!-- Галерея -->
      <div class="gallery">
        <UICarouselGallery :items="product.images" />
      </div>

      <!-- Информация о товаре -->
      <div class="info">
        <h1 class="title">{{ product.name }}</h1>

        <div class="brand">Бренд: {{ product.brand }}</div>

        <div class="rating" v-if="product.rating">
          ⭐ {{ product.rating }}/{{ product.max_rating }}
        </div>

        <div class="price">{{ product.price.full }}</div>

        <div
            class="availability"
            :class="{ in_stock: product.availability_status === 'in_stock' }"
        >
          {{ product.availability }}
        </div>

        <UIButton variant="primary" size="lg" block>
          В корзину
        </UIButton>
      </div>

    </div>

    <!-- ===== Tabs ===== -->
    <div class="section mt-10">
      <UTabs v-model="activeTab">

        <!-- Заголовки табов -->
        <UTabList>
          <UTab name="description">Описание</UTab>
          <UTab name="features">Характеристики</UTab>
          <UTab name="reviews">Отзывы</UTab>
        </UTabList>

        <!-- Контент табов -->
        <UTabPanels>

          <!-- Описание -->
          <UTabPanel name="description">
            <div class="tab-content">
              <p v-html="product.description" class="description"/>
            </div>
          </UTabPanel>

          <!-- Характеристики -->
          <UTabPanel name="features">
            <table class="features">
              <tbody>
              <tr v-for="f in product.features" :key="f.name">
                <td class="f-name">{{ f.name }}</td>
                <td class="f-value">{{ f.value }}</td>
              </tr>
              </tbody>
            </table>
          </UTabPanel>

          <!-- Отзывы -->
          <UTabPanel name="reviews">
            <div class="reviews-placeholder">
              Отзывов пока нет 😔
            </div>
          </UTabPanel>

        </UTabPanels>
      </UTabs>
    </div>

  </div>
</template>

<script setup lang="ts">
import { productMock } from '~/data/mocks/products'
import type { ProductData } from '~/types/product'

const product: ProductData = productMock

const activeTab = ref('description')

const breadcrumbs = ref([
  { label: 'Каталог', to: '/catalog' },
  { label: product.brand, to: `/catalog?brand=${product.brand}` },
  { label: product.name }
])
</script>

<style scoped>
.breadcrumb{
  margin-bottom: 20px;
}

.top-block {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
}

@media (max-width: 900px) {
  .top-block {
    grid-template-columns: 1fr;
  }
}

.info {
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.title {
  font-size: 28px;
  font-weight: bold;
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
  font-weight: bold;
  color: var(--color-accent);
}

.availability {
  font-size: 15px;
}
.availability.in_stock {
  color: #28a745;
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
  background: rgba(0, 0, 0, 0.04);
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
}

.reviews-placeholder {
  padding: 20px;
  font-size: 15px;
  color: var(--color-gray-dark);
  background: rgba(0,0,0,0.05);
  border-radius: 10px;
}
</style>