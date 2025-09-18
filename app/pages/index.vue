<script setup lang="ts">
import type { FormData } from '~/server/api/form.get'
import { useBreakpoints } from '@vueuse/core'

const { data } = await useFetch<FormData>('/api/form')

const lycee = ref(data.value?.lycee ?? '')
const classe = ref<string | null>(data.value?.classe ?? null)
const bac = ref<string | null>(data.value?.type ?? null)

const tempClasse = ref(classe.value)
const tempBac = ref(bac.value)

const isClasseOpen = ref(false)

const breakpoints = useBreakpoints({ lg: 1024 })
const isDesktop = breakpoints.greater('lg')

const confirmClasse = () => {
  classe.value = tempClasse.value
  bac.value = tempBac.value
  isClasseOpen.value = false
}

watch(isClasseOpen, (open) => {
  if (!open) {
    tempClasse.value = classe.value
    tempBac.value = bac.value
  }
})
</script>

<template>
  <div class="flex-1 w-full flex flex-col gap-4 items-stretch">
    <div class="w-full max-w-3xl flex flex-col gap-4 self-center flex-1">
      <EMSchoolCard :lycee="lycee" location="Lille" type="Lycée Public" />

      <EMAccordion
          v-model:open="isClasseOpen"
          title="Classe"
          :description="classe && bac ? `${classe}, ${bac}` : undefined"
          :show-description="!!classe && !!bac"
          helper="À compléter"
          :show-helper="!classe || !bac"
      >
        <EMButtonGroup
            :options="['Seconde', 'Première', 'Terminale']"
            v-model="tempClasse"
        />

        <EMSeparator />

        <EMButtonGroup
            label="Type de bac"
            :options="['Général', 'Technologique', 'Professionnel']"
            v-model="tempBac"
        />

        <div class="pt-4">
          <EMButton
              full-width
              variant="primary"
              :disabled="!tempClasse || !tempBac"
              @click="confirmClasse"
          >
            Confirmer
          </EMButton>
        </div>
      </EMAccordion>

      <EMAccordion title="Spécialités" helper="À compléter" :show-helper="true" />
      <EMAccordion title="Notes" helper="À compléter" :show-helper="true" />
        <div v-if="isDesktop" class="w-full flex justify-center">
        <EMButton  variant="primary" :disabled="!classe || !bac">
          Confirmer
        </EMButton>
      </div>
    </div>

    <div v-if="!isDesktop" class=" w-full flex justify-center">
      <EMButton  variant="primary" :disabled="!classe || !bac">
        Confirmer
      </EMButton>
    </div>
  </div>
</template>