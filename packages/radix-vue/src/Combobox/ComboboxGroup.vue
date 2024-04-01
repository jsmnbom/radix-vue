<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'
import { createContext, useForwardExpose, useId } from '@/shared'
import { useMutationObserver } from '@vueuse/core'
import { comboboxRootContext } from './ComboboxRoot.vue'

export interface ComboboxGroupProps extends PrimitiveProps {}

type ComboboxGroupContext = {
  id: string
}

export const comboboxGroupContext = createContext<ComboboxGroupContext>('ComboboxGroup')
</script>

<script setup lang="ts">
import { nextTick, ref, watch } from 'vue'
import { Primitive } from '@/Primitive'

const props = defineProps<ComboboxGroupProps>()

const { currentRef, currentElement } = useForwardExpose()
const id = useId(undefined, 'radix-vue-combobox-group')

const rootContext = comboboxRootContext.inject()
const hasOptions = ref(false)

function checkCollectionItem() {
  if (!currentElement.value)
    return

  const collectionItem = currentElement.value.querySelectorAll('[data-radix-vue-combobox-item]:not([data-hidden])')
  hasOptions.value = !!collectionItem.length
}

useMutationObserver(currentElement, () => {
  checkCollectionItem()
}, { childList: true })

watch(() => rootContext.searchTerm.value, () => {
  nextTick(() => {
    checkCollectionItem()
  })
}, { immediate: true })

comboboxGroupContext.provide({
  id,
})
</script>

<template>
  <Primitive
    v-show="hasOptions"
    v-bind="props"
    ref="currentRef"
    role="group"
    :aria-labelledby="id"
  >
    <slot />
  </Primitive>
</template>
