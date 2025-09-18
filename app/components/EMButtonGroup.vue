<script setup lang="ts">
const props = defineProps<{
  label?: string
  options: string[]
  modelValue?: string | string[] | null
  multiple?: boolean
}>()

const emit = defineEmits<{
  (e: "update:modelValue", value: string | string[]): void
}>()

const toggle = (opt: string) => {
  if (props.multiple) {
    const current = Array.isArray(props.modelValue)
        ? [...props.modelValue]
        : []
    emit(
        "update:modelValue",
        current.includes(opt)
            ? current.filter(o => o !== opt)
            : [...current, opt]
    )
  } else {
    emit("update:modelValue", opt)
  }
}

const isSelected = (opt: string) => {
  if (props.multiple) {
    return (
        Array.isArray(props.modelValue) && props.modelValue.includes(opt)
    )
  }
  return props.modelValue === opt
}
</script>

<template>
  <div class="flex flex-col gap-4 w-full">
    <p v-if="label" class="text-sm font-medium">{{ label }}</p>

    <div class="flex flex-wrap gap-2">
      <EMButton
          v-for="opt in options"
          :key="opt"
          size="sm"
          variant="secondary"
          :selected="isSelected(opt)"
          type="button"
          @click="toggle(opt)"
      >
        {{ opt }}
      </EMButton>
    </div>
  </div>
</template>