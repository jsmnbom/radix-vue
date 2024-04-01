<script lang="ts">
import type { PrimitiveProps } from '@/Primitive'
import { tagsInputItemContext } from './TagsInputItem.vue'
import { tagsInputRootContext } from './TagsInputRoot.vue'
import { computed } from 'vue'
import { useForwardExpose } from '@/shared'

export interface TagsInputItemDeleteProps extends PrimitiveProps {}
</script>

<script setup lang="ts">
import { Primitive } from '@/Primitive'

const props = withDefaults(defineProps<TagsInputItemDeleteProps>(), {
  as: 'button',
})

useForwardExpose()
const context = tagsInputRootContext.inject()
const itemContext = tagsInputItemContext.inject()

const disabled = computed(() => itemContext.disabled?.value || context.disabled.value)

function handleDelete() {
  if (disabled.value)
    return
  const index = context.modelValue.value.findIndex(i => i === itemContext.value.value)
  context.onRemoveValue(index)
}
</script>

<template>
  <Primitive
    tabindex="-1"
    v-bind="props"
    :aria-labelledby="itemContext.textId"
    :aria-current="itemContext.isSelected.value"
    :data-state="itemContext.isSelected.value ? 'active' : 'inactive'"
    :data-disabled="disabled ? '' : undefined"
    :type="as === 'button' ? 'button' : undefined"
    @click="handleDelete"
  >
    <slot />
  </Primitive>
</template>
