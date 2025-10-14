<script setup lang="ts">
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])

function onInput(e: Event) {
  const v = Number((e.target as HTMLInputElement).value)
  emit('update:modelValue', Number.isNaN(v) ? 0 : v)
}

function onBlur() {
  const v = Number(props.modelValue)
  const sanitized = Math.min(99, Math.max(10, Number.isNaN(v) ? 10 : v))
  emit('update:modelValue', sanitized)
}
</script>

<template>
  <div class="input_container">
    <label for="age">your age</label>
    <input
      type="number"
      name="age"
      :value="props.modelValue"
      min="10"
      max="99"
      @input="onInput"
      @blur="onBlur"
    />
  </div>
</template>

<style scoped>
input[type='number']::-webkit-outer-spin-button,
input[type='number']::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
input[type='number'] {
  -moz-appearance: textfield;
  appearance: textfield;
  width: 15px;
}

.input_container {
  display: flex;
  gap: 5px;
  align-items: baseline;
}
</style>
