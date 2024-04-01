<script lang="ts">
import type { PopperArrowProps } from '@/Popper'

export interface SelectArrowProps extends PopperArrowProps {}
</script>

<script setup lang="ts">
import { selectRootContext } from './SelectRoot.vue'
import { selectContentContext } from './SelectContentImpl.vue'
import { PopperArrow } from '@/Popper'

const props = withDefaults(defineProps<SelectArrowProps>(), {
  width: 10,
  height: 5,
  as: 'svg',
})
const rootContext = selectRootContext.inject()
const contentContext = selectContentContext.inject()
</script>

<template>
  <PopperArrow
    v-if="rootContext.open.value && contentContext.position === 'popper'"
    v-bind="props"
  >
    <slot />
  </PopperArrow>
</template>
