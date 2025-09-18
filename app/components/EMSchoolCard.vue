<script setup lang="ts">
import { ref, computed, watch, nextTick } from 'vue';

const props = defineProps<{
  lycee: string;
  location?: string;
  type?: string;
  lycees: string[];
}>();

const emit = defineEmits(['update:lycee']);

const editing = ref(false);
const query = ref(props.lycee);
const inputRef = ref<HTMLInputElement | null>(null);

const filteredLycees = computed(() => {
  if (!query.value) {
    return props.lycees;
  }
  return props.lycees.filter(l =>
      l.toLowerCase().includes(query.value.toLowerCase())
  );
});

const selectLycee = (name: string) => {
  emit('update:lycee', name);
  query.value = name;
  editing.value = false;
};

const activateEditing = async () => {
  editing.value = true;
  query.value = props.lycee;
  await nextTick();
  if (inputRef.value) {
    inputRef.value.focus();
  }
};

const cancelEditing = () => {
  editing.value = false;
  query.value = props.lycee;
};

const handleInputBlur = () => {
  setTimeout(() => {
    const isValidSelection = props.lycees.some(l => l.toLowerCase() === query.value.toLowerCase());
    if (editing.value && !isValidSelection) {
      cancelEditing();
    } else if (editing.value) {
      editing.value = false;
    }
  }, 150);
};

watch(() => props.lycee, (newLycee) => {
  if (!editing.value) {
    query.value = newLycee;
  }
}, { immediate: true });
</script>

<template>
  <div
      class="w-full max-w-[720px] rounded-xl bg-gradient-to-r from-[#FF7342] to-[#B176FF] text-white p-5 flex flex-col gap-3 sm:flex-row sm:justify-between sm:items-start"
  >
    <!-- Bloc gauche (nom du lycée ou input autocomplete) -->
    <div class="flex flex-col gap-2 relative w-full sm:w-auto">
      <h2 v-if="!editing" class="font-semibold text-lg">
        {{ lycee }}
      </h2>
      <div v-else class="relative w-full">
        <input
            ref="inputRef"
            v-model="query"
            type="text"
            placeholder="Rechercher un lycée..."
            class="rounded px-3 py-2 text-[#212121] w-full"
            @blur="handleInputBlur"
            @keydown.enter.prevent="filteredLycees.length > 0 && selectLycee(filteredLycees[0])"
        />
        <ul
            v-if="query && filteredLycees.length > 0"
            class="absolute top-full left-0 right-0 bg-white text-[#212121] rounded shadow max-h-48 overflow-y-auto z-20 mt-1"
        >
          <li
              v-for="l in filteredLycees"
              :key="l"
              @mousedown.prevent="selectLycee(l)"
              class="px-3 py-2 hover:bg-gray-100 cursor-pointer"
          >
            {{ l }}
          </li>
        </ul>
      </div>

      <div class="flex items-center gap-1 text-sm opacity-90">
        <Icon name="mdi:map-marker" /> <span>{{ location ?? 'Lille' }}</span>
        <span>• {{ type ?? 'Lycée Public' }}</span>
      </div>
    </div>

    <!-- Bloc droit : bouton Modifier / Annuler -->
    <div class="flex-shrink-0">
      <EMButton
          v-if="!editing"
          size="sm"
          variant="secondary"
          @click="activateEditing"
      >
        Modifier
      </EMButton>
      <EMButton
          v-else
          size="sm"
          variant="secondary"
          @click="cancelEditing"
      >
        Annuler
      </EMButton>
    </div>
  </div>
</template>