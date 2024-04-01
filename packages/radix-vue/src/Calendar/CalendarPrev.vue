<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface CalendarPrevProps extends PrimitiveProps { }
</script>

<script setup lang="ts">
import { Primitive } from '@/Primitive'
import { calendarRootContext } from './CalendarRoot.vue'

const props = withDefaults(defineProps<CalendarPrevProps>(), { as: 'button' })

const rootContext = calendarRootContext.inject()
</script>

<template>
  <Primitive
    aria-label="Previous page"
    v-bind="props"
    :type="as === 'button' ? 'button' : undefined"
    :aria-disabled="rootContext.isPrevButtonDisabled.value || undefined"
    :data-disabled="rootContext.isPrevButtonDisabled.value || undefined"
    :disabled="rootContext.isPrevButtonDisabled.value"
    @click="rootContext.prevPage"
  >
    <slot>Prev page</slot>
  </Primitive>
</template>
