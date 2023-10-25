<template>
  <div class="card">
    <slot/>
  </div>
</template>

<script setup lang="ts">

</script>

<style scoped>
.card {
  padding: 23px 55px 40px;
  border-radius: 16px;
  border: 1px solid #000;
  background: #FFF;
  box-shadow: 0 4px 4px 0 rgba(0, 0, 0, .25);
}
</style>