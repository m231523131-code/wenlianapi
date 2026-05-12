<template>
  <div class="card overflow-hidden">
    <div class="border-b border-primary-100/70 bg-gradient-to-r from-primary-50 to-accent-50/70 px-6 py-4 dark:border-dark-700 dark:from-primary-950/40 dark:to-accent-950/20">
      <h2 class="text-lg font-black tracking-tight text-primary-950 dark:text-white">{{ t('dashboard.quickActions') }}</h2>
    </div>
    <div class="space-y-3 p-4">
      <button @click="router.push('/keys')" class="group flex w-full items-center gap-4 rounded-2xl bg-primary-50/70 p-4 text-left ring-1 ring-primary-100/80 transition-all duration-200 hover:-translate-y-0.5 hover:bg-primary-100 dark:bg-dark-800/50 dark:ring-dark-700 dark:hover:bg-dark-800">
        <div class="flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-2xl bg-gradient-to-br from-primary-500 to-primary-800 text-white shadow-lg shadow-primary-500/20 transition-transform group-hover:scale-105">
          <Icon name="key" size="lg" class="text-white" />
        </div>
        <div class="min-w-0 flex-1">
          <p class="text-sm font-medium text-gray-900 dark:text-white">{{ t('dashboard.createApiKey') }}</p>
          <p class="text-xs text-gray-500 dark:text-dark-400">{{ t('dashboard.generateNewKey') }}</p>
        </div>
        <Icon
          name="chevronRight"
          size="md"
          class="text-gray-400 transition-colors group-hover:text-primary-500 dark:text-dark-500"
        />
      </button>

      <button @click="router.push('/usage')" class="group flex w-full items-center gap-4 rounded-2xl bg-primary-50/70 p-4 text-left ring-1 ring-primary-100/80 transition-all duration-200 hover:-translate-y-0.5 hover:bg-primary-100 dark:bg-dark-800/50 dark:ring-dark-700 dark:hover:bg-dark-800">
        <div class="flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-2xl bg-gradient-to-br from-sky-500 to-primary-700 text-white shadow-lg shadow-primary-500/20 transition-transform group-hover:scale-105">
          <Icon name="chart" size="lg" class="text-white" />
        </div>
        <div class="min-w-0 flex-1">
          <p class="text-sm font-medium text-gray-900 dark:text-white">{{ t('dashboard.viewUsage') }}</p>
          <p class="text-xs text-gray-500 dark:text-dark-400">{{ t('dashboard.checkDetailedLogs') }}</p>
        </div>
        <Icon
          name="chevronRight"
          size="md"
          class="text-gray-400 transition-colors group-hover:text-emerald-500 dark:text-dark-500"
        />
      </button>

      <button @click="router.push('/redeem')" class="group flex w-full items-center gap-4 rounded-2xl bg-accent-50/80 p-4 text-left ring-1 ring-accent-100/90 transition-all duration-200 hover:-translate-y-0.5 hover:bg-accent-100 dark:bg-dark-800/50 dark:ring-dark-700 dark:hover:bg-dark-800">
        <div class="flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-2xl bg-gradient-to-br from-accent-300 to-accent-600 text-white shadow-lg shadow-accent-500/20 transition-transform group-hover:scale-105">
          <Icon name="gift" size="lg" class="text-white" />
        </div>
        <div class="min-w-0 flex-1">
          <p class="text-sm font-medium text-gray-900 dark:text-white">{{ t('dashboard.redeemCode') }}</p>
          <p class="text-xs text-gray-500 dark:text-dark-400">{{ t('dashboard.addBalanceWithCode') }}</p>
        </div>
        <Icon
          name="chevronRight"
          size="md"
          class="text-gray-400 transition-colors group-hover:text-amber-500 dark:text-dark-500"
        />
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useRouter } from 'vue-router'
import { useI18n } from 'vue-i18n'
import Icon from '@/components/icons/Icon.vue'
const router = useRouter()
const { t } = useI18n()
</script>
