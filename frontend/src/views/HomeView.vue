<template>
  <!-- Custom Home Content: Full Page Mode -->
  <div v-if="homeContent" class="min-h-screen">
    <iframe
      v-if="isHomeContentUrl"
      :src="homeContent.trim()"
      class="h-screen w-full border-0"
      allowfullscreen
    ></iframe>
    <div v-else v-html="homeContent"></div>
  </div>

  <!-- Wenlianapi Default Home Page -->
  <div v-else class="min-h-screen overflow-hidden bg-[#f4efe3] text-[#12100b]">
    <div class="pointer-events-none fixed inset-0">
      <div class="absolute inset-0 bg-[radial-gradient(circle_at_20%_15%,rgba(255,196,71,0.35),transparent_24rem),radial-gradient(circle_at_80%_10%,rgba(39,117,255,0.18),transparent_22rem),linear-gradient(135deg,#f8f2e6,#eef4ff_56%,#f7e7c5)]"></div>
      <div class="absolute inset-0 opacity-[0.28] bg-[linear-gradient(rgba(18,16,11,0.08)_1px,transparent_1px),linear-gradient(90deg,rgba(18,16,11,0.08)_1px,transparent_1px)] bg-[size:42px_42px]"></div>
    </div>

    <header class="relative z-20 px-5 py-5">
      <nav class="mx-auto flex max-w-7xl items-center justify-between rounded-full border border-black/10 bg-white/70 px-4 py-3 shadow-[0_20px_60px_rgba(33,27,14,0.08)] backdrop-blur-xl">
        <router-link to="/" class="flex items-center gap-3">
          <div class="flex h-11 w-11 items-center justify-center rounded-2xl bg-[#12100b] text-lg font-black text-[#ffc447] shadow-lg shadow-black/20">
            <img v-if="siteLogo" :src="siteLogo" alt="Logo" class="h-full w-full rounded-2xl object-contain" />
            <span v-else>W</span>
          </div>
          <div class="hidden sm:block">
            <div class="text-sm font-black uppercase tracking-[0.2em]">{{ siteName }}</div>
            <div class="text-xs text-black/50">GPT API Service</div>
          </div>
        </router-link>

        <div class="flex items-center gap-2">
          <a
            v-if="docUrl"
            :href="docUrl"
            target="_blank"
            rel="noopener noreferrer"
            class="hidden rounded-full px-4 py-2 text-sm font-semibold text-black/60 transition hover:bg-black/5 hover:text-black md:inline-flex"
          >
            {{ t('home.docs') }}
          </a>
          <LocaleSwitcher />
          <button
            @click="toggleTheme"
            class="rounded-full p-2 text-black/50 transition hover:bg-black/5 hover:text-black"
            :title="isDark ? t('home.switchToLight') : t('home.switchToDark')"
          >
            <Icon v-if="isDark" name="sun" size="md" />
            <Icon v-else name="moon" size="md" />
          </button>
          <router-link
            :to="isAuthenticated ? dashboardPath : '/login'"
            class="rounded-full bg-[#12100b] px-5 py-2 text-sm font-bold text-white shadow-lg shadow-black/20 transition hover:-translate-y-0.5 hover:bg-black"
          >
            {{ isAuthenticated ? t('home.dashboard') : t('home.login') }}
          </router-link>
        </div>
      </nav>
    </header>

    <main class="relative z-10">
      <section class="mx-auto grid max-w-7xl items-center gap-10 px-5 pb-12 pt-10 lg:grid-cols-[1.05fr_0.95fr] lg:pb-20 lg:pt-16">
        <div>
          <div class="mb-6 inline-flex items-center gap-3 rounded-full border border-black/10 bg-white/75 px-4 py-2 text-xs font-black uppercase tracking-[0.2em] shadow-sm">
            <span class="h-2.5 w-2.5 rounded-full bg-emerald-500 shadow-[0_0_0_6px_rgba(16,185,129,0.12)]"></span>
            当前仅开放 GPT
          </div>
          <h1 class="max-w-4xl text-5xl font-black leading-[0.95] tracking-[-0.06em] text-[#12100b] md:text-7xl lg:text-8xl">
            专注 GPT 的 API 接入平台
          </h1>
          <p class="mt-7 max-w-2xl text-lg leading-8 text-black/60 md:text-xl">
            {{ siteName }} 只面向 GPT 系列模型提供接入、密钥管理、用量统计和余额控制。用户拿到一个 API Key，就能按你的规则稳定使用 GPT。
          </p>
          <div class="mt-9 flex flex-col gap-3 sm:flex-row">
            <router-link
              :to="isAuthenticated ? dashboardPath : '/login'"
              class="group inline-flex items-center justify-center rounded-2xl bg-[#246bfe] px-7 py-4 text-base font-black text-white shadow-[0_24px_50px_rgba(36,107,254,0.28)] transition hover:-translate-y-1 hover:bg-[#1457df]"
            >
              {{ isAuthenticated ? '进入控制台' : '获取 GPT API Key' }}
              <Icon name="arrowRight" size="md" class="ml-2 transition group-hover:translate-x-1" />
            </router-link>
            <router-link
              v-if="!isAuthenticated"
              to="/register"
              class="inline-flex items-center justify-center rounded-2xl border border-black/10 bg-white/75 px-7 py-4 text-base font-black text-[#12100b] shadow-sm transition hover:-translate-y-1 hover:bg-white"
            >
              注册账号
            </router-link>
          </div>
        </div>

        <div class="relative">
          <div class="absolute -right-8 -top-8 h-32 w-32 rounded-full bg-[#ffc447] blur-2xl"></div>
          <div class="relative overflow-hidden rounded-[2.25rem] border border-black/10 bg-[#12100b] p-5 text-white shadow-[0_35px_90px_rgba(18,16,11,0.35)]">
            <div class="mb-5 flex items-center justify-between">
              <div>
                <div class="text-xs font-black uppercase tracking-[0.22em] text-[#ffc447]">GPT Console</div>
                <div class="mt-1 text-2xl font-black">接入面板</div>
              </div>
              <div class="rounded-full bg-emerald-400/20 px-3 py-1 text-xs font-bold text-emerald-300">
                GPT 已启用
              </div>
            </div>

            <div class="space-y-3">
              <div class="rounded-2xl border border-white/10 bg-white/10 p-4">
                <div class="mb-2 text-xs uppercase tracking-[0.18em] text-white/50">Base URL</div>
                <div class="font-mono text-sm text-white/90">https://api.wenlianapi.cn/v1</div>
              </div>
              <div class="grid grid-cols-2 gap-3">
                <div class="rounded-2xl border border-white/10 bg-white/10 p-4">
                  <div class="text-xs text-white/50">支持范围</div>
                  <div class="mt-2 text-xl font-black">GPT</div>
                </div>
                <div class="rounded-2xl border border-white/10 bg-white/10 p-4">
                  <div class="text-xs text-white/50">计费方式</div>
                  <div class="mt-2 text-xl font-black">按量</div>
                </div>
              </div>
              <div class="rounded-2xl bg-[#ffc447] p-4 text-[#12100b]">
                <div class="text-xs font-black uppercase tracking-[0.18em]">Ready</div>
                <div class="mt-2 text-lg font-black">创建密钥后即可调用 GPT 接口</div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section class="relative mx-auto max-w-7xl px-5 pb-16">
        <div class="grid gap-4 md:grid-cols-3">
          <div class="rounded-[2rem] border border-black/10 bg-white/70 p-6 shadow-sm backdrop-blur-xl">
            <div class="mb-5 flex h-12 w-12 items-center justify-center rounded-2xl bg-[#246bfe] text-white">
              <Icon name="key" size="lg" />
            </div>
            <h3 class="text-xl font-black">一个 Key 接入 GPT</h3>
            <p class="mt-3 text-sm leading-6 text-black/60">
              用户无需理解复杂配置，创建 API Key 后按 OpenAI 兼容格式调用。
            </p>
          </div>
          <div class="rounded-[2rem] border border-black/10 bg-white/70 p-6 shadow-sm backdrop-blur-xl">
            <div class="mb-5 flex h-12 w-12 items-center justify-center rounded-2xl bg-[#12100b] text-[#ffc447]">
              <Icon name="shield" size="lg" />
            </div>
            <h3 class="text-xl font-black">账号池稳定调度</h3>
            <p class="mt-3 text-sm leading-6 text-black/60">
              后台继续保留账号调度、额度、分组等能力，用户侧只感知稳定服务。
            </p>
          </div>
          <div class="rounded-[2rem] border border-black/10 bg-white/70 p-6 shadow-sm backdrop-blur-xl">
            <div class="mb-5 flex h-12 w-12 items-center justify-center rounded-2xl bg-[#ffc447] text-[#12100b]">
              <Icon name="chart" size="lg" />
            </div>
            <h3 class="text-xl font-black">用量清晰可查</h3>
            <p class="mt-3 text-sm leading-6 text-black/60">
              余额、请求量、Token 和成本继续在控制台展示，方便用户自助查看。
            </p>
          </div>
        </div>
      </section>

      <section class="relative border-y border-black/10 bg-[#12100b] px-5 py-14 text-white">
        <div class="mx-auto flex max-w-7xl flex-col gap-8 md:flex-row md:items-center md:justify-between">
          <div>
            <div class="text-xs font-black uppercase tracking-[0.24em] text-[#ffc447]">Supported Model</div>
            <h2 class="mt-3 text-3xl font-black tracking-tight md:text-5xl">当前仅支持 GPT</h2>
            <p class="mt-4 max-w-2xl text-sm leading-7 text-white/60">
              其他模型暂未开放，用户侧只展示 GPT，避免产生“都能用”的误解。
            </p>
          </div>
          <div class="rounded-[2rem] border border-white/10 bg-white/10 p-5">
            <div class="flex items-center gap-4">
              <div class="flex h-14 w-14 items-center justify-center rounded-2xl bg-emerald-500 text-xl font-black">G</div>
              <div>
                <div class="text-2xl font-black">GPT</div>
                <div class="mt-1 text-sm text-emerald-300">已开放使用</div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>

    <footer class="relative z-10 px-5 py-8">
      <div class="mx-auto flex max-w-7xl flex-col gap-4 text-sm text-black/50 sm:flex-row sm:items-center sm:justify-between">
        <p>&copy; {{ currentYear }} {{ siteName }}. {{ t('home.footer.allRightsReserved') }}</p>
        <a v-if="docUrl" :href="docUrl" target="_blank" rel="noopener noreferrer" class="font-semibold hover:text-black">
          {{ t('home.docs') }}
        </a>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { useI18n } from 'vue-i18n'
import { useAuthStore, useAppStore } from '@/stores'
import LocaleSwitcher from '@/components/common/LocaleSwitcher.vue'
import Icon from '@/components/icons/Icon.vue'

const { t } = useI18n()

const authStore = useAuthStore()
const appStore = useAppStore()

const siteName = computed(() => appStore.cachedPublicSettings?.site_name || appStore.siteName || 'wenlianapi')
const siteLogo = computed(() => appStore.cachedPublicSettings?.site_logo || appStore.siteLogo || '')
const docUrl = computed(() => appStore.cachedPublicSettings?.doc_url || appStore.docUrl || '')
const homeContent = computed(() => appStore.cachedPublicSettings?.home_content || '')

const isHomeContentUrl = computed(() => {
  const content = homeContent.value.trim()
  return content.startsWith('http://') || content.startsWith('https://')
})

const isDark = ref(document.documentElement.classList.contains('dark'))
const isAuthenticated = computed(() => authStore.isAuthenticated)
const isAdmin = computed(() => authStore.isAdmin)
const dashboardPath = computed(() => (isAdmin.value ? '/admin/dashboard' : '/dashboard'))
const currentYear = computed(() => new Date().getFullYear())

function toggleTheme() {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('dark', isDark.value)
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
}

function initTheme() {
  const savedTheme = localStorage.getItem('theme')
  if (
    savedTheme === 'dark' ||
    (!savedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches)
  ) {
    isDark.value = true
    document.documentElement.classList.add('dark')
  }
}

onMounted(() => {
  initTheme()
  authStore.checkAuth()
  if (!appStore.publicSettingsLoaded) {
    appStore.fetchPublicSettings()
  }
})
</script>
