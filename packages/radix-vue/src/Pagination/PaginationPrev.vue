<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'
import { useForwardExpose } from '@/shared'

export interface PaginationPrevProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { Primitive } from '@/Primitive'
import { paginationRootContext } from './PaginationRoot.vue'

const props = withDefaults(defineProps<PaginationPrevProps>(), { as: 'button' })

useForwardExpose()
const rootContext = paginationRootContext.inject()
</script>

<template>
  <Primitive
    v-bind="props"
    aria-label="Previous Page"
    :type="as === 'button' ? 'button' : undefined"
    :disabled="rootContext.page.value === 1 || rootContext.disabled?.value"
    @click="rootContext.onPageChange(rootContext.page.value - 1)"
  >
    <slot>Prev page</slot>
  </Primitive>
</template>
