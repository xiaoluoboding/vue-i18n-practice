<template>
  <h1>{{ $t('common.home') }}</h1>

  <button type="button" @click="toggleLocales">Toggle Language</button>
</template>

<script setup lang="ts">
import { useI18n } from 'vue-i18n'
import { useLocalStorage } from '@vueuse/core'

const { availableLocales, locale } = useI18n()
const setLang = (lang: string) => {
  const storage = useLocalStorage('site_locale', '')
  storage.value = lang
}

const toggleLocales = () => {
  const locales = availableLocales
  locale.value = locales[(locales.indexOf(locale.value) + 1) % locales.length]
  setLang(locale.value)
}
</script>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
