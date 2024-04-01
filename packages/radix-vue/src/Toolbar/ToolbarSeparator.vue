<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'

export interface ToolbarSeparatorProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { useForwardExpose } from '@/shared'
import BaseSeparator from '../shared/component/BaseSeparator.vue'
import { toolbarRootContext } from './ToolbarRoot.vue'

const props = defineProps<ToolbarSeparatorProps>()

const rootContext = toolbarRootContext.inject()
useForwardExpose()
</script>

<template>
  <BaseSeparator
    :orientation="rootContext.orientation.value"
    :as-child="props.asChild"
    :as="as"
  >
    <slot />
  </BaseSeparator>
</template>
