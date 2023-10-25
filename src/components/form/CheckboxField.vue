<template>
  <div class="field">
    <label :for="id.toString()">
      <input
        type="checkbox"
        :id="id.toString()"
        :value="modelValue"
        @change="emit('update:modelValue', !modelValue)"
      >
      <span class="field__label">
        <slot>{{ label }}</slot>
      </span>
    </label>
  </div>
</template>

<script setup lang="ts">
export interface Props {
  id: string | number;
  label?: string;
  modelValue: boolean;
}

export interface Emits {
  (e: 'update:modelValue', val: boolean): void;
}

const props = defineProps<Props>();
const emit = defineEmits<Emits>();
</script>


<style scoped>
.field label {
    display: flex;
    align-items: center;
    gap: 20px;
    font-size: 16px;
    text-align: center;
}

.field input {
    position: relative;
    display: block;
    width: 18px;
    height: 18px;
    appearance: none;
    border-radius: 9px;
    border: 1px solid #05AC6A;
    background: #FFF;
    cursor: pointer;
}

.field input:checked::before {
    display: block;
    position: absolute;
    content: '';
    top: 50%;
    left: 50%;
    width: 14px;
    height: 14px;
    border-radius: 50%;
    background: #05AC6A;
    transform: translate(-50%, -50%);
}
</style>
