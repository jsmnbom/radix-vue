<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface ComboboxCancelProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { Primitive } from '@/Primitive'
import { useForwardExpose } from '@/shared'
import { comboboxRootContext } from './ComboboxRoot.vue'

const props = withDefaults(defineProps<ComboboxCancelProps>(), {
  as: 'button',
})

useForwardExpose()
const rootContext = comboboxRootContext.inject()

function handleClick() {
  rootContext.searchTerm.value = ''
  rootContext.inputElement.value?.focus()
}
</script>

<template>
  <Primitive
    :type="as === 'button' ? 'button' : undefined"
    v-bind="props"
    tabindex="-1"
    @click="handleClick"
  >
    <slot />
  </Primitive>
</template>
