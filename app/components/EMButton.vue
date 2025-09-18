<script setup lang="ts">
const props = defineProps<{
  size?: "sm" | "md"
  variant?: "primary" | "secondary"
  fullWidth?: boolean
  disabled?: boolean
  selected?: boolean
}>()
</script>

<template>
  <button
      :disabled="disabled"
      :class="[
      'inline-flex justify-center items-center font-medium transition focus:outline-none rounded-full cursor-pointer',
      size === 'sm' ? 'px-4 py-2 text-sm h-8' : 'px-6 py-4 text-base h-12',
      variant === 'primary'
        ? 'bg-[#212121] text-white hover:bg-gray-900 disabled:bg-white disabled:text-gray-400 disabled:border disabled:border-gray-200 cursor-not-allowed'
        : [
            'bg-gray-100 text-gray-800 hover:bg-gray-200 disabled:text-gray-400 disabled:opacity-50',
            'border',
            selected ? 'border-[#212121] bg-white text-[#212121]' : 'border-transparent',
            disabled ? 'cursor-not-allowed' : 'cursor-pointer'
          ],
      fullWidth ? 'w-full' : 'w-auto',
    ]"
      v-bind="$attrs"
  >
    <slot />
  </button>
</template>
