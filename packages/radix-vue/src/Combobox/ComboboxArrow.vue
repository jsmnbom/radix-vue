<script lang="ts">
import type { PopperArrowProps } from '@/Popper'

export interface ComboboxArrowProps extends PopperArrowProps {}
</script>

<script setup lang="ts">
import { comboboxRootContext } from './ComboboxRoot.vue'
import { comboboxContentContext } from './ComboboxContentImpl.vue'
import { useForwardExpose } from '@/shared'
import { PopperArrow } from '@/Popper'

const props = withDefaults(defineProps<ComboboxArrowProps>(), {
  width: 10,
  height: 5,
  as: 'svg',
})
const rootContext = comboboxRootContext.inject()
const contentContext = comboboxContentContext.inject()

useForwardExpose()
</script>

<template>
  <PopperArrow
    v-if="rootContext.open.value && contentContext.position.value === 'popper'"
    v-bind="props"
  >
    <slot />
  </PopperArrow>
</template>
