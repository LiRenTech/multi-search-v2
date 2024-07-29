<template>
  <n-space vertical>
    <n-space>
      <n-input v-model="query" />
      <n-button @click="search">search</n-button>
    </n-space>
  </n-space>
</template>

<script setup lang="ts">
const query = ref('');
const router = useRouter();

const search = () => {
  router.push({
    path: '/search',
    query: {
      q: query.value,
    },
  });
};
</script>
