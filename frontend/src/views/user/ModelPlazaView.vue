<template>
  <AppLayout>
    <div class="space-y-6">
      <section class="rounded-3xl border border-gray-200/70 bg-white/85 p-6 shadow-sm backdrop-blur-sm dark:border-dark-700/70 dark:bg-dark-900/75">
        <div class="flex flex-col gap-4 lg:flex-row lg:items-end lg:justify-between">
          <div>
            <div class="mb-3 inline-flex items-center gap-2 rounded-full bg-primary-50 px-3 py-1 text-xs font-semibold text-primary-700 dark:bg-primary-900/20 dark:text-primary-300">
              <img :src="openaiMark" alt="OpenAI" class="h-4 w-4 rounded-sm object-contain" />
              {{ t('modelPlaza.badge') }}
            </div>
            <h2 class="text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
              {{ t('modelPlaza.heading') }}
            </h2>
            <p class="mt-2 max-w-3xl text-sm leading-relaxed text-gray-600 dark:text-dark-300">
              {{ t('modelPlaza.intro') }}
            </p>
          </div>
          <div class="rounded-2xl border border-primary-100 bg-primary-50/80 px-4 py-3 text-sm text-primary-800 dark:border-primary-900/40 dark:bg-primary-900/10 dark:text-primary-200">
            <p class="font-semibold">{{ t('modelPlaza.priceNoteTitle') }}</p>
            <p class="mt-1">{{ t('modelPlaza.priceNoteBody') }}</p>
          </div>
        </div>
      </section>

      <section class="grid gap-5 md:grid-cols-2 xl:grid-cols-3">
        <article
          v-for="model in models"
          :key="model.id"
          class="group flex h-full flex-col rounded-3xl border border-gray-200/80 bg-white p-5 shadow-sm transition-all duration-200 hover:-translate-y-0.5 hover:shadow-lg dark:border-dark-700/80 dark:bg-dark-900"
        >
          <div class="flex items-start gap-4">
            <div class="flex h-16 w-16 items-center justify-center rounded-2xl border border-gray-200 bg-gray-50 shadow-sm dark:border-dark-700 dark:bg-dark-800">
              <img :src="openaiMark" alt="OpenAI" class="h-10 w-10 rounded-xl object-contain" />
            </div>
            <div class="min-w-0">
              <h3 class="break-all text-xl font-bold tracking-tight text-gray-900 dark:text-white">
                {{ model.id }}
              </h3>
              <p class="mt-2 text-sm leading-7 text-gray-700 dark:text-dark-200">
                {{ t('modelPlaza.inputPrice') }} {{ formatPrice(model.inputPrice) }} / 1M Tokens
              </p>
              <p class="text-sm leading-7 text-gray-700 dark:text-dark-200">
                {{ t('modelPlaza.outputPrice') }} {{ formatPrice(model.outputPrice) }} / 1M Tokens
              </p>
              <p class="text-sm leading-7 text-gray-700 dark:text-dark-200">
                {{ t('modelPlaza.cacheReadPrice') }} {{ formatPrice(model.cacheReadPrice) }} / 1M Tokens
              </p>
            </div>
          </div>

          <div class="mt-5 flex flex-wrap gap-2">
            <span class="rounded-full bg-violet-100 px-3 py-1 text-xs font-semibold text-violet-700 dark:bg-violet-900/25 dark:text-violet-300">
              {{ t('modelPlaza.billingTag') }}
            </span>
          </div>
        </article>
      </section>
    </div>
  </AppLayout>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'
import AppLayout from '@/components/layout/AppLayout.vue'
import openaiMark from '@/assets/icons/openai-mark.svg'

interface ModelCard {
  id: string
  inputPrice: number
  outputPrice: number
  cacheReadPrice: number
}

const { t } = useI18n()

const models = computed<ModelCard[]>(() => [
  {
    id: 'gpt-5.1',
    inputPrice: 1.25,
    outputPrice: 10,
    cacheReadPrice: 0.125,
  },
  {
    id: 'gpt-5.1-codex',
    inputPrice: 1.25,
    outputPrice: 10,
    cacheReadPrice: 0.125,
  },
  {
    id: 'gpt-5.1-codex-max',
    inputPrice: 1.25,
    outputPrice: 10,
    cacheReadPrice: 0.125,
  },
  {
    id: 'gpt-5.1-codex-mini',
    inputPrice: 0.25,
    outputPrice: 2,
    cacheReadPrice: 0.025,
  },
  {
    id: 'gpt-5.2',
    inputPrice: 1.75,
    outputPrice: 14,
    cacheReadPrice: 0.175,
  },
  {
    id: 'gpt-5.2-codex',
    inputPrice: 1.75,
    outputPrice: 14,
    cacheReadPrice: 0.175,
  },
  {
    id: 'gpt-5.3',
    inputPrice: 1.75,
    outputPrice: 14,
    cacheReadPrice: 0.175,
  },
  {
    id: 'gpt-5.3-codex',
    inputPrice: 1.75,
    outputPrice: 14,
    cacheReadPrice: 0.175,
  },
  {
    id: 'gpt-5.4',
    inputPrice: 2.5,
    outputPrice: 15,
    cacheReadPrice: 0.25,
  },
])

function formatPrice(value: number): string {
  return `$${value.toFixed(4)}`
}
</script>
