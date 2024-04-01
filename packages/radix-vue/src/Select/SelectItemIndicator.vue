<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface SelectItemIndicatorProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { selectItemContext } from './SelectItem.vue'
import { Primitive } from '@/Primitive'

const props = withDefaults(defineProps<SelectItemIndicatorProps>(), {
  as: 'span',
})

const itemContext = selectItemContext.inject()
</script>

<template>
  <Primitive v-if="itemContext.isSelected.value" aria-hidden v-bind="props">
    <slot />
  </Primitive>
</template>
