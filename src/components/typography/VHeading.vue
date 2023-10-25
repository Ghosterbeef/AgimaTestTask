<template>
  <RenderFunction/>
</template>

<script setup lang="ts">
import {h} from 'vue';

export interface Props {
  level?: 1 | 2 | 3 | '1' | '2' | '3';
  align?: 'center' | 'right' | 'left'
  bottomOffset?: boolean;
}

const {level = 1, bottomOffset = false, align = 'center'} = defineProps<Props>();
const slots = defineSlots();

const RenderFunction = h(`h${level}`, {
    class: [
      `h${level}`,
      `_${align}`,
      {
        '_bottom-offset': bottomOffset,
      }
    ]
  },
  {default: slots.default}
)
</script>

<style>
:is(.h1, .h2, .h3)._center {
    text-align: center;
}

:is(.h1, .h2, .h3)._left {
    text-align: left;
}

:is(.h1, .h2, .h3)._right {
    text-align: right;
}

.h1 {
    font-size: 42px;
}

.h2 {
    font-size: 24px;
}

.h3 {
    font-size: 22px;
}

.h2._bottom-offset {
    margin-bottom: 57px;
}
</style>
