<script setup lang="ts">
const props = defineProps<{
  size?: "sm" | "md"
  variant?: "primary" | "secondary"
  fullWidth?: boolean
  disabled?: boolean
}>()
</script>

<template>
  <button
      :disabled="disabled"
      :class="[
      'inline-flex justify-center items-center font-medium transition focus:outline-none rounded-full',
      size === 'sm' ? 'px-4 py-2 text-sm h-8' : 'px-6 py-4 text-base h-12',
      variant === 'primary'
        ? 'bg-[#212121] text-white hover:bg-gray-900 disabled:bg-white disabled:text-gray-400 disabled:border disabled:border-gray-200'
        : 'bg-white text-[#212121] border border-gray-300 hover:bg-gray-50 disabled:text-gray-400 disabled:border-gray-200',
      fullWidth ? 'w-full' : 'w-auto',
    ]"
  >
    <slot />
  </button>
</template>