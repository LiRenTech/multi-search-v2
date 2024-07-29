<template>
  <n-config-provider :theme="darkTheme" :locale="zhCN" :date-locale="dateZhCN">
    <n-dialog-provider>
      <router-view />
    </n-dialog-provider>
    <n-global-style />
  </n-config-provider>
</template>

<script setup lang="ts">
import { lightTheme, darkTheme, zhCN, dateZhCN } from 'naive-ui';
import { RouterView } from 'vue-router';

const theme = ref(lightTheme);

onMounted(() => {
  window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', (event) => {
    theme.value = event.matches ? darkTheme : lightTheme;
  });
});
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
