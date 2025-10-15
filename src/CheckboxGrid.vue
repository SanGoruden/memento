<script setup lang="ts">
import { computed, ref } from 'vue'
import CheckboxInput from './CheckboxInput.vue'
import Progressbar from './ProgressBar.vue'

const baseTotal = ref(3806)
const age = ref(24)
const n_checked = computed(() => age.value * 52)
const progressPercentage = computed(() => Math.min(100, Math.max(0, (n_checked.value / 3806) * 100)))
const ttl = computed(() => Math.max(3806 - n_checked.value, 0))
const sleep = ref(false) // 33%
const work = ref(false) // 12%

const totalLength = computed(() => {
  let v = baseTotal.value
  if (sleep.value) v -= ttl.value / 3
  if (work.value) v -= ttl.value * 0.12
  return Math.max(0, Math.round(v))
})

const array = computed(() =>
  Array.from({ length: totalLength.value }, (_, i) => (i < n_checked.value ? 1 : 0)),
)
</script>

<template>
  <div class="checkbox_grid_container">
    <div class="checkbox_grid_header">
      <CheckboxInput v-model="age" />
      <div class="checkbox_grid_header_buttons_container">
        <div class="checkbox_grid_header_button" @click="sleep = !sleep">
          {{ sleep ? 'x sleep' : '_ sleep' }}
        </div>
        <div class="checkbox_grid_header_button" @click="work = !work">
          {{ work ? 'x work' : '_ work' }}
        </div>
      </div>
    </div>
    <div class="checkbox_grid">
      <input v-for="(item, index) in array" :key="index" type="checkbox" :checked="item === 1" disabled />
    </div>
    <div class="progress_wrapper">
      <Progressbar :percentage="progressPercentage" :ttl="ttl" />
    </div>
  </div>
  <div v-if="!ttl" class="checkbox_grid_footer_text">you lived longer than expected :)</div>
</template>

<style scoped>
.checkbox_grid_container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 10px);
  gap: 2px;
  align-content: start;
  justify-content: start;
}

.checkbox_grid_header,
.checkbox_grid,
.progress_wrapper {
  grid-column: 1 / -1;
}

.progress_wrapper {
  width: 50%;
  justify-self: center;
}

.checkbox_grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, 10px);
  gap: 2px;
  width: 100%;
  align-content: start;
  justify-content: start;
}

.checkbox_grid input[type='checkbox'] {
  width: 10px;
  height: 10px;
  margin: 0;
}

.checkbox_grid_header {
  margin-top: 15px;
  margin-bottom: 10px;
  display: flex;
  justify-content: space-between;
}

.checkbox_grid_header_button {
  display: inline;
  cursor: pointer;
  user-select: none;
  width: min-content;
  white-space: nowrap;
  display: inline-block;
}

.checkbox_grid_header_button:hover {
  text-decoration: underline;
}

.checkbox_grid_header_buttons_container {
  display: flex;
  gap: 20px;
}

.checkbox_grid_footer_text {
  margin-top: 5px;
  justify-self: center;
}

.progress_wrapper {
  margin-top: 10px;
}
</style>
