<template>
  <div class="app-layout">
    <LayoutHeader />
    <main class="main-content">
      <slot />
    </main>
    <LayoutFooter />
  </div>
</template>

<script setup></script>

<style scoped>
.app-layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.main-content {
  flex: 1;
  padding: 20px;
}
</style>