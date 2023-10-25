<template>
  <div class="flip-card" :class="{'flip-card--flipped': flipped}">
    <slot></slot>
  </div>
</template>

<script setup lang="ts">
export interface Props {
  flipped: boolean;
}

defineProps<Props>();
</script>

<style scoped>
.flip-card {
    position: relative;
    display: grid;
    transition: 250ms;
    background-color: transparent;
    transform-style: preserve-3d;
}

.flip-card--flipped {
    transform: rotateY(-180deg);
}

.flip-card > :slotted(*:nth-child(1)),
.flip-card > :slotted(*:nth-child(2)) {
    grid-area: 1 / 1 / 2 / 2;
    backface-visibility: hidden;
}

.flip-card > :slotted(*:nth-child(1)) {
    z-index: 2;
}

.flip-card > :slotted(*:nth-child(2)) {
    z-index: 1;
    transform: rotateY(180deg);
}
</style>
