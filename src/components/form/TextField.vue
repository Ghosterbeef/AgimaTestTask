<template>
  <div class="field">
    <input type="text" :id="id.toString()" :class="{filled: modelValue}" :value="modelValue"
           @input="emit('update:modelValue', ($event.target as HTMLInputElement).value)">
    <label :for="id.toString()">{{ placeholder }}</label>
  </div>
</template>

<script setup lang="ts">
export interface Props {
  id: string | number;
  placeholder?: string;
  modelValue: string;
}

export interface Emits {
  (e: 'update:modelValue', val: string): void;
}

const props = defineProps<Props>();
const emit = defineEmits<Emits>();
</script>

<style scoped>
.field {
  display: grid;
  justify-items: flex-start;
  align-items: center;
  font-size: 22px;
  margin: 32px 0;
}

.field input {
  grid-area: 1 / 1/ 2/ 2;
  min-width: min(520px, 90vw);
  padding: 15px 16px;
  border: none;
  border-bottom: 1px solid #000;
  background: #FFF;
  font-size: 22px;
  font-family: inherit;
  outline: none;
}

.field label {
  grid-area: 1 / 1/ 2/ 2;
  pointer-events: none;
  transition: 250ms;
  margin-left: 16px;
}

.field input:focus + label {
  transform: translateY(-75%);
  color: #05AC6A;
}

.field input:not(:focus).filled + label {
  opacity: 0;
}
</style>