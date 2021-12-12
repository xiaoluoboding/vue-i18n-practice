<template>
  <h1>{{ $t('common.home') }}</h1>
  
  <p>{{ $t('header.title') }}</p>

  <p>{{ $t('message.hello', { msg }) }}</p>

  <button type="button" @click="toggleLocales">{{ $t('button.toggle-language') }}</button>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'
import { useLocalStorage } from '@vueuse/core'

const msg = ref('')

const { availableLocales, locale } = useI18n()
const setLang = (lang: string) => {
  const storage = useLocalStorage('site_locale', '')
  storage.value = lang
}

const toggleLocales = () => {
  const locales = availableLocales
  locale.value = locales[(locales.indexOf(locale.value) + 1) % locales.length]
  setLang(locale.value)
  if (locale.value === 'en') {
    msg.value = 'Hello'
  } else {
    msg.value = '你好'
  }
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
