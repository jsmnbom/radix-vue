<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface AccordionHeaderProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { useForwardExpose } from '@/shared'
import { accordionItemContext } from './AccordionItem.vue'
import { accordionRootContext } from './AccordionRoot.vue'
import { Primitive } from '@/Primitive'

const props = withDefaults(defineProps<AccordionHeaderProps>(), {
  as: 'h3',
})

const rootContext = accordionRootContext.inject()
const itemContext = accordionItemContext.inject()

useForwardExpose()
</script>

<template>
  <Primitive
    :as="props.as"
    :as-child="props.asChild"
    :data-orientation="rootContext.orientation"
    :data-state="itemContext.dataState.value"
    :data-disabled="itemContext.dataDisabled.value"
  >
    <slot />
  </Primitive>
</template>
