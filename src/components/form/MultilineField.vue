<template>
  <div class="field">
    <div class="icon" v-if="$slots.icon">
      <slot name="icon"/>
    </div>
    <textarea
      :id="id.toString()"
      :value="modelValue"
      :placeholder="placeholder"
      :disabled="disabled"
      @input="emit('update:modelValue', ($event.target as HTMLInputElement).value)"
    />
    <slot name="append"/>
  </div>
</template>

<script setup lang="ts">
export interface Props {
  id: string | number;
  placeholder?: string;
  modelValue: string;
  disabled?: boolean;
}

export interface Emits {
  (e: 'update:modelValue', val: string): void;
}

const props = defineProps<Props>();
const emit = defineEmits<Emits>();
</script>

<style scoped>
.field {
    position: relative;
    display: flex;
    gap: 8px;
    flex-direction: column;
}

.field textarea {
    resize: none;
    border-radius: 8px;
    border: 1px solid #000;
    background: #FFF;
    min-width: min(520px, 90vw);
    padding: 15px 16px;
    height: 168px;
    outline: none;
    font-size: 22px;
    font-family: inherit;
}

.field textarea::placeholder {
    font-size: 22px;
    font-family: inherit;
    color: #000000;
}

.field textarea:focus::placeholder {
    opacity: 0;
}

.field textarea:disabled {
    background: #ECECEC;
}

.field textarea:disabled::placeholder {
    opacity: 0;
}


.field .icon {
    position: absolute;
    top: 6px;
    right: 8px;
}
</style>
