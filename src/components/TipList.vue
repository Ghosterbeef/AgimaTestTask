<template>
  <ul class="tip-list">
    <slot></slot>
  </ul>
</template>

<style scoped>
.tip-list {
    display: flex;
    flex-direction: column;
    gap: 24px;
    list-style: none;
}
</style>
