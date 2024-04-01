<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface HoverCardTriggerProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { hoverCardRootContext } from './HoverCardRoot.vue'
import { Primitive } from '@/Primitive'
import { PopperAnchor } from '@/Popper'
import { useForwardExpose } from '@/shared'
import { excludeTouch } from './utils'

withDefaults(defineProps<HoverCardTriggerProps>(), {
  as: 'a',
})

const { forwardRef, currentElement } = useForwardExpose()
const rootContext = hoverCardRootContext.inject()
rootContext.triggerElement = currentElement
</script>

<template>
  <PopperAnchor as-child>
    <Primitive
      :ref="forwardRef"
      :as-child="asChild"
      :as="as"
      :data-state="rootContext.open.value ? 'open' : 'closed'"
      @pointerenter="excludeTouch(rootContext.onOpen)($event)"
      @focus="rootContext.onOpen()"
      @blur="rootContext.onClose"
      @touchstart.prevent="() => {
        // prevent focus event on touch devices
      }"
    >
      <slot />
    </Primitive>
  </PopperAnchor>
</template>
