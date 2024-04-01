<script setup lang="ts">
import TooltipContentImpl, { type TooltipContentImplProps } from './TooltipContentImpl.vue'
import { tooltipRootContext } from './TooltipRoot.vue'
import { tooltipProviderContext } from './TooltipProvider.vue'
import { useForwardExpose, useForwardProps, useGraceArea } from '@/shared'

const props = defineProps<TooltipContentImplProps>()
const forwardedProps = useForwardProps(props)
const { forwardRef, currentElement } = useForwardExpose()

const { trigger, onClose } = tooltipRootContext.inject()
const providerContext = tooltipProviderContext.inject()

const { isPointerInTransit, onPointerExit } = useGraceArea(trigger, currentElement)

providerContext.isPointerInTransitRef = isPointerInTransit
onPointerExit(() => {
  onClose()
})
</script>

<template>
  <TooltipContentImpl :ref="forwardRef" v-bind="forwardedProps">
    <slot />
  </TooltipContentImpl>
</template>
