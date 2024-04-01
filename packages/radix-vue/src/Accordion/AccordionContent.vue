<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface AccordionContentProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { useForwardExpose } from '@/shared'
import { CollapsibleContent } from '../Collapsible'
import { accordionItemContext } from './AccordionItem.vue'
import { accordionRootContext } from './AccordionRoot.vue'

const props = defineProps<AccordionContentProps>()

const rootContext = accordionRootContext.inject()
const itemContext = accordionItemContext.inject()

useForwardExpose()
</script>

<template>
  <CollapsibleContent
    role="region"
    :open="itemContext.open.value"
    :hidden="!itemContext.open.value"
    :as-child="props.asChild"
    :aria-labelledby="itemContext.triggerId"
    :data-state="itemContext.dataState.value"
    :data-disabled="itemContext.dataDisabled.value"
    :data-orientation="rootContext.orientation"
    style="
      --radix-accordion-content-width: var(--radix-collapsible-content-width);
      --radix-accordion-content-height: var(--radix-collapsible-content-height);
    "
  >
    <slot />
  </CollapsibleContent>
</template>
