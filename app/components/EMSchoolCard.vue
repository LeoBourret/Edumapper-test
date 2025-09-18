<script setup lang="ts">
defineProps<{
  lycee: string
  location?: string
  type?: string
}>()
</script>

<template>
  <div
      class="w-full max-w-[720px] rounded-xl bg-gradient-to-r from-[#FF7342] to-[#B176FF] text-white p-5 flex flex-col gap-6 shadow-md"
  >
    <h2 class="font-semibold text-lg">{{ lycee }}</h2>

    <div class="flex items-center gap-1 text-sm opacity-90">
      <Icon name="mdi:map-marker" />
      <span>{{ location ?? 'Lille' }}</span>
      <span>• {{ type ?? 'Lycée Public' }}</span>
    </div>

    <div>
      <EMButton size="sm" variant="secondary">
        Modifier
      </EMButton>
    </div>
  </div>
</template>