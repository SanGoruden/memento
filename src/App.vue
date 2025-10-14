<script setup lang="ts">
import BottomText from './BottomText.vue'
import CheckboxGrid from './CheckboxGrid.vue'
</script>

<template>
  <div class="page">
    <div class="header">
      <h1>memento</h1>
      <img src="/skull.png" alt="skull" />
    </div>
    <CheckboxGrid />
    <BottomText />
  </div>
</template>

<style scoped>
.page {
  max-width: 1000px;
  margin: 0 auto;
  padding: 24px 16px;
}

h1 {
  font-size: 50px;
  margin: 75px 0 0 40px;
  user-select: none;
}

.header {
  display: flex;
  justify-content: space-between;
}

.header img {
  width: 95px;
  z-index: -1;
  position: absolute;
}
</style>
