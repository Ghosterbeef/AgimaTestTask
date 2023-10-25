<template>
  <div class="field" :class="{_disabled: disabled}">
    <label :for="id.toString()">{{ label }}
      <input ref="inputRef" :id="id.toString()" type="file" :disabled="disabled" @change="onChange">
      <span v-if="modelValue">{{ modelValue.name }}</span>
    </label>
    <IconDelete v-if="modelValue" @click="emit('update:modelValue', null)"/>
  </div>
</template>

<script setup lang="ts">
import {ref} from "vue";
import IconDelete from "@/components/icons/IconDelete.vue";

export interface Props {
  id: string | number;
  label?: string;
  modelValue: File | null;
  disabled?: boolean;
}

export interface Emits {
  (e: 'update:modelValue', val: File | null): void;
}

const props = defineProps<Props>();
const emit = defineEmits<Emits>();

const inputRef = ref<HTMLInputElement | null>(null);

function onChange() {
  emit('update:modelValue', inputRef.value?.files?.[0] ?? null)
}
</script>

<style scoped>
.field._disabled label {
  color: #6F6F6F;
  cursor: default;
}

.field label {
  font-size: 22px;
  color: #000000;
  transition: 250ms;
  cursor: pointer;
}

.field label:hover {
  color: #05AC6A;
}

.field input {
  position: absolute;
  opacity: 0;
  z-index: -1;
}
</style>
