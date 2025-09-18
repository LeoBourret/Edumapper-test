<script setup lang="ts">
const props = defineProps<{
  title: string
  helper?: string
  description?: string
  showHelper?: boolean
  showDescription?: boolean
  open?: boolean
}>()

const emit = defineEmits(['update:open'])

const isOpen = computed({
  get: () => props.open ?? false,
  set: (val: boolean) => emit('update:open', val)
})

const toggle = () => (isOpen.value = !isOpen.value)
</script>

<template>
  <div class="w-full max-w-[720px] rounded-xl bg-white border border-gray-200 p-5 shadow-sm">
    <button @click="toggle" class="w-full flex justify-between items-center cursor-pointer">
      <div class="flex flex-col items-start">
        <div class="font-semibold text-gray-900">{{ title }}</div>
        <div v-if="!isOpen && showDescription && description" class="text-sm text-gray-700">
          {{ description }}
        </div>
      </div>

      <div class="flex items-center gap-2 text-sm text-gray-500">
        <span v-if="!isOpen && showHelper && helper">{{ helper }}</span>
        <span :class="isOpen ? 'rotate-180' : ''">▼</span>
      </div>
    </button>

    <div v-if="isOpen" class="mt-6 space-y-6">
      <slot />
    </div>
  </div>
</template>