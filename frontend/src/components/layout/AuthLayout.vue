<template>
  <div class="relative flex min-h-screen items-center justify-center overflow-hidden bg-[#07111f] p-4 text-slate-100">
    <!-- Background -->
    <div
      class="absolute inset-0 bg-[radial-gradient(circle_at_15%_20%,rgba(47,130,246,0.32),transparent_28rem),radial-gradient(circle_at_85%_12%,rgba(247,173,22,0.22),transparent_22rem),linear-gradient(135deg,#061120,#102441_58%,#07111f)]"
    ></div>

    <!-- Decorative Elements -->
    <div class="pointer-events-none absolute inset-0 overflow-hidden">
      <!-- Gradient Orbs -->
      <div
        class="absolute -right-40 -top-40 h-80 w-80 rounded-full bg-accent-400/20 blur-3xl"
      ></div>
      <div
        class="absolute -bottom-40 -left-40 h-80 w-80 rounded-full bg-primary-400/25 blur-3xl"
      ></div>
      <div
        class="absolute left-1/2 top-1/2 h-96 w-96 -translate-x-1/2 -translate-y-1/2 rounded-full bg-white/5 blur-3xl"
      ></div>

      <!-- Grid Pattern -->
      <div
        class="absolute inset-0 bg-[linear-gradient(rgba(255,255,255,0.045)_1px,transparent_1px),linear-gradient(90deg,rgba(255,255,255,0.045)_1px,transparent_1px)] bg-[size:72px_72px]"
      ></div>
    </div>

    <!-- Content Container -->
    <div class="relative z-10 w-full max-w-md">
      <!-- Logo/Brand -->
      <div class="mb-8 text-center">
        <!-- Custom Logo or Default Logo -->
        <template v-if="settingsLoaded">
          <div
            class="mb-4 inline-flex h-16 w-16 items-center justify-center overflow-hidden rounded-[1.35rem] bg-gradient-to-br from-primary-400 via-primary-700 to-accent-400 text-2xl font-black text-white shadow-lg shadow-primary-500/30 ring-1 ring-white/20"
          >
            <img v-if="siteLogo" :src="siteLogo" alt="Logo" class="h-full w-full object-contain" />
            <span v-else>W</span>
          </div>
          <h1 class="mb-2 text-3xl font-black tracking-tight text-white">
            {{ siteName }}
          </h1>
          <p class="text-sm text-slate-300">
            {{ siteSubtitle }}
          </p>
          <div class="mt-4 flex items-center justify-center gap-2 text-[11px] font-semibold uppercase tracking-[0.22em] text-accent-200/90">
            <span class="h-px w-8 bg-accent-300/50"></span>
            <span>AI Access Console</span>
            <span class="h-px w-8 bg-accent-300/50"></span>
          </div>
        </template>
      </div>

      <!-- Card Container -->
      <div class="rounded-[1.75rem] border border-white/20 bg-white/95 p-8 text-gray-900 shadow-2xl shadow-black/25 backdrop-blur-xl dark:bg-slate-950/80 dark:text-gray-100">
        <slot />
      </div>

      <!-- Footer Links -->
      <div class="mt-6 text-center text-sm">
        <slot name="footer" />
      </div>

      <!-- Copyright -->
      <div class="mt-8 text-center text-xs text-slate-400">
        &copy; {{ currentYear }} {{ siteName }}. All rights reserved.
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, onMounted } from 'vue'
import { useAppStore } from '@/stores'
import { sanitizeUrl } from '@/utils/url'

const appStore = useAppStore()

const siteName = computed(() => appStore.siteName || '稳连API')
const siteLogo = computed(() => sanitizeUrl(appStore.siteLogo || '', { allowRelative: true, allowDataUrl: true }))
const siteSubtitle = computed(() => appStore.cachedPublicSettings?.site_subtitle || 'API 中转站')
const settingsLoaded = computed(() => appStore.publicSettingsLoaded)

const currentYear = computed(() => new Date().getFullYear())

onMounted(() => {
  appStore.fetchPublicSettings()
})
</script>

<style scoped>
.text-gradient {
  @apply bg-gradient-to-r from-primary-600 to-primary-500 bg-clip-text text-transparent;
}
</style>
