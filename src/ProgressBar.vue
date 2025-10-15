<script setup lang="ts">
import { computed } from 'vue'

const props = withDefaults(defineProps<{ percentage?: number }>(), {
  percentage: 0,
})

const clamped = computed(() => Math.min(100, Math.max(0, props.percentage ?? 0)))
</script>

<template>
  <div
    class="progressbar"
    role="progressbar"
    :aria-valuenow="clamped"
    aria-valuemin="0"
    aria-valuemax="100"
  >
    <div class="fill" :style="{ width: clamped + '%' }"></div>
  </div>
</template>

<style scoped>
.progressbar {
  height: 9px;
  background: #eee;
  position: relative;
  overflow: hidden;
}

.fill {
  height: 100%;
  background: black;
  width: 0%;
  transition: width 300ms ease;
}

.label {
  position: absolute;
  right: 8px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 12px;
  color: #fff;
  text-shadow: 0 1px 0 rgba(0, 0, 0, 0.3);
}
</style>
