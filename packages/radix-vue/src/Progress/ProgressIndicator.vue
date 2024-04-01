<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'
import { useForwardExpose } from '@/shared'

export interface ProgressIndicatorProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { progressRootContext } from './ProgressRoot.vue'
import { Primitive } from '@/Primitive'

const props = defineProps<ProgressIndicatorProps>()

const rootContext = progressRootContext.inject()
useForwardExpose()
</script>

<template>
  <Primitive
    v-bind="props"
    :data-state="rootContext.progressState.value"
    :data-value="rootContext.modelValue?.value ?? undefined"
    :data-max="rootContext.max.value"
  >
    <slot />
  </Primitive>
</template>
