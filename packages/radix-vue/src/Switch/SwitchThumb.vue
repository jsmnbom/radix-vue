<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'
import { useForwardExpose } from '@/shared'

export interface SwitchThumbProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { switchRootContext } from './SwitchRoot.vue'
import { Primitive } from '@/Primitive'

withDefaults(defineProps<SwitchThumbProps>(), { as: 'span' })

const rootContext = switchRootContext.inject()

useForwardExpose()
</script>

<template>
  <Primitive
    :data-state="rootContext.checked?.value ? 'checked' : 'unchecked'"
    :data-disabled="rootContext.disabled.value ? '' : undefined"
    :as-child="asChild"
    :as="as"
  >
    <slot />
  </Primitive>
</template>
