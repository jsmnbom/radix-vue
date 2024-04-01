<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface RangeCalendarPrevProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { Primitive } from '@/Primitive'
import { rangeCalendarRootContext } from './RangeCalendarRoot.vue'

const props = withDefaults(defineProps<RangeCalendarPrevProps>(), { as: 'button' })

const rootContext = rangeCalendarRootContext.inject()
</script>

<template>
  <Primitive
    v-bind="props"
    aria-label="Previous page"
    :type="as === 'button' ? 'button' : undefined"
    :aria-disabled="rootContext.isPrevButtonDisabled.value || undefined"
    :data-disabled="rootContext.isPrevButtonDisabled.value || undefined"
    :disabled="rootContext.isPrevButtonDisabled.value"
    @click="rootContext.prevPage"
  >
    <slot>Prev page</slot>
  </Primitive>
</template>
