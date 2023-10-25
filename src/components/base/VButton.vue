<template>
  <button class="button" :class="{_disabled: disabled}">
    <slot></slot>
  </button>
</template>

<script setup lang="ts">
import type {ButtonHTMLAttributes} from "vue";

export interface Props {
  type?: ButtonHTMLAttributes['type'];
  disabled?: boolean;
}

withDefaults(defineProps<Props>(), {
  type: 'button',
  disabled: false
});
</script>

<style scoped>
.button {
    display: flex;
    gap: 10px;
    align-items: center;
    border-radius: 8px;
    background: #05AC6A;
    padding: 0 20px;
    height: 56px;
    cursor: pointer;
    transition: 250ms;
    font: inherit;
    font-size: 16px;
    border: none;
    outline: none;
    color: #FFFFFF;
}

.button._disabled {
    background: #6F6F6F;
}
</style>
