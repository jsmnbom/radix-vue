<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'
import { useForwardExpose } from '@/shared'

export interface DialogTitleProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { dialogRootContext } from './DialogRoot.vue'
import { Primitive } from '@/Primitive'

const props = withDefaults(defineProps<DialogTitleProps>(), { as: 'h2' })
const rootContext = dialogRootContext.inject()
useForwardExpose()
</script>

<template>
  <Primitive v-bind="props" :id="rootContext.titleId">
    <slot />
  </Primitive>
</template>
