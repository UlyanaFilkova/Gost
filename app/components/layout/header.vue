<script setup lang="ts">
import type { NavigationMenuItem } from '@nuxt/ui'
const route = useRoute()

/** Пункты меню строго по NavigationMenuItem */
const items = computed<NavigationMenuItem[]>(() => [
  {
    label: 'Главная',
    to: '/',
    active: route.path === '/'
  },
  {
    label: 'Каталог',
    to: '/catalog/',
    active: route.path.startsWith('/catalog')
  },
  {
    label: 'Поиск',
    to: '/search/',
    active: route.path.startsWith('/search')
  },
  {
    label: 'Бренды',
    to: '/brand/',
    active: route.path.startsWith('/brand')
  },
  {
    label: 'Акции',
    to: '/sales/',
    active: route.path.startsWith('/sales')
  },
  {
    label: 'Оплата и доставка',
    to: '/delivery/',
    active: route.path.startsWith('/delivery')
  },
  {
    label: 'Контакты',
    to: '/contacts/',
    active: route.path.startsWith('/contacts')
  },
  {
    label: 'Вход',
    to: '/auth/',
    active: route.path.startsWith('/auth')
  }
])
</script>

<template>
  <header class="header">
    <!-- верхняя полоса -->
    <div class="top-bar">
      <div class="container">
        <div class="row">
          <div class="col-left">
            <p class="location">
              <span class="fa fa-map-marker" />
              Беларусь, г. Витебск, пр-т Фрунзе, 39а, к.17
            </p>
          </div>

          <div class="col-right">
            <div class="basket">
              <a href="/order/">
                <span id="basket-status">
                  <i class="fa fa-shopping-basket" /> В корзине нет товаров
                </span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Nuxt UI Header -->
    <UHeader class="main-header">
      <!-- Логотип -->
      <template #title>
        <a class="navbar-brand" href="/">Gost.By</a>
      </template>

      <!-- Desktop меню -->
      <UNavigationMenu
          :items="items"
          class="desktop-menu"
      />

      <!-- Правая часть -->
      <template #right>
        <UColorModeButton />
      </template>

      <!-- Mobile меню -->
      <template #body>
        <UNavigationMenu
            :items="items"
            orientation="vertical"
            class="mobile-menu -mx-2.5"
        />
      </template>
    </UHeader>
  </header>
</template>

<style scoped>

/* ---------------- Верхняя панель ---------------- */

.top-bar {
  background: #f5f5f5;
  padding: 8px 0;
  font-size: 14px;
}

.location .fa {
  margin-right: 6px;
}

.row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Корзина */
.basket .fa {
  margin-right: 5px;
}

/* ---------------- Основной хедер ---------------- */

.main-header {
  background: #2c3e50 !important;
  color: white;
}

.navbar-brand {
  font-size: 22px;
  text-decoration: none;
  color: white;
}

/* Desktop меню */
.desktop-menu {
  display: flex;
}

/* Mobile скрыто */
.mobile-menu {
  display: none;
}

/* ---------------- Адаптив ---------------- */

@media (max-width: 768px) {
  .desktop-menu {
    display: none !important;
  }

  .mobile-menu {
    display: block !important;
  }
}

</style>
