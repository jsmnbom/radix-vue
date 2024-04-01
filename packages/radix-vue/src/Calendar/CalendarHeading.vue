<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface CalendarHeadingProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { Primitive } from '@/Primitive'
import { calendarRootContext } from './CalendarRoot.vue'

const props = withDefaults(defineProps<CalendarHeadingProps>(), { as: 'div' })

defineSlots<{
  default(props: {
    /** Current month and year */
    headingValue: string
  }): any
}>()

const rootContext = calendarRootContext.inject()
</script>

<template>
  <Primitive
    v-bind="props"
    :data-disabled="rootContext.disabled.value ? '' : undefined"
  >
    <slot :heading-value="rootContext.headingValue.value">
      {{ rootContext.headingValue.value }}
    </slot>
  </Primitive>
</template>
