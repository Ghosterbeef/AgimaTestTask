<template>
  <li class="tip-list__item">
    <VHeading level="3" class="tip-list__item-title" align="left">{{ title }}</VHeading>
    <p class="tip-list__item-text">
      {{ text }}
    </p>
  </li>
</template>

<script setup lang="ts">
import VHeading from "@/components/typography/VHeading.vue";

export interface Props {
  title: string;
  text: string;
}

defineProps<Props>();
</script>

<style scoped>
.tip-list__item {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.tip-list__item-text {
    margin-left: 22px;
    white-space: pre-wrap;
}
</style>
