<template>
  <div class="min-h-screen bg-[#F7F3F0] flex flex-col justify-between">
    <EMHeader />
    <main class="flex-1 w-full flex flex-col p-4 sm:p-6 lg:p-[24px]">
      <slot />
    </main>
  </div>
</template>