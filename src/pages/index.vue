<template>
  <div class="container">
    <n-space vertical>
      <h1>Multi Search</h1>
      <n-space>
        <n-input v-model:value="query" />
        <n-button @click="search">搜索</n-button>
      </n-space>
      <n-divider />
      <n-collapse accordion>
        <n-collapse-item title="编程类"><n-transfer v-model:value="selected1" :options="engines1" /></n-collapse-item>
        <n-collapse-item title="文学类"><n-transfer v-model:value="selected2" :options="engines2" /></n-collapse-item>
        <n-collapse-item title="自定义">
          <n-space vertical>
            <n-transfer v-model:value="selected3" :options="engines3" />
            <n-divider>设置</n-divider>
            <n-input v-model:value="customName" placeholder="搜索引擎名称" />
            <n-input v-model:value="customUrl" placeholder="URL (搜索关键词占位符: %%%)" />
            <n-space>
              <n-button type="info" @click="addCustom">添加</n-button>
              <n-button type="error" @click="deleteCustom">删除已选</n-button>
            </n-space>
          </n-space>
        </n-collapse-item>
      </n-collapse>
    </n-space>
  </div>
</template>

<script setup lang="ts">
const query = ref('');
const selected1 = ref<string[]>([]);
const selected2 = ref<string[]>([]);
const selected3 = ref<string[]>([]);
const customName = ref('');
const customUrl = ref('');

const search = () => {
  for (const url of [...selected1.value, ...selected2.value, ...selected3.value]) {
    window.open(url.replace('%%%', query.value), '_blank');
  }
};

const addCustom = () => {
  if (customName.value && customUrl.value) {
    engines3.value.push({ value: customUrl.value, label: customName.value });
    customName.value = '';
    customUrl.value = '';
  }
};
const deleteCustom = () => {
  engines3.value = engines3.value.filter((engine) => !selected3.value.includes(engine.value));
};

const engines1 = [
  {
    value: 'https://bing.com/search?q=%%%',
    label: 'Bing',
  },
  {
    value: 'https://www.google.com/search?q=%%%',
    label: 'Google',
  },
  {
    value: 'https://www.baidu.com/s?wd=%%%',
    label: '百度',
  },
  {
    value: 'https://search.bilibili.com/all?keyword=%%%',
    label: 'Bilibili',
  },
  {
    value: 'https://www.zhihu.com/search?type=content&q=%%%',
    label: '知乎',
  },
  {
    value: 'https://www.xiaohongshu.com/search_result?keyword=%%%',
    label: '小红书',
  },
  {
    value: 'https://kaifa.baidu.com/searchPage?wd=%%%',
    label: '百度开发者',
  },
  {
    value: 'https://so.csdn.net/so/search?t=all&u=&q=%%%',
    label: 'CSDN',
  },
  {
    value: 'https://www.jianshu.com/search?page=1&type=note&q=%%%',
    label: '简书',
  },
  {
    value: 'https://github.com/search?type=code&q=%%%',
    label: 'GitHub',
  },
];
const engines2 = [
  {
    value: 'https://www.loc.gov/collections/world-digital-library/?q=%%%',
    label: 'LOC World Digital Library',
  },
  {
    value: 'https://www.fastsoso.cc/search?k=%%%',
    label: 'Fastsoso网盘搜索',
  },
  {
    value: 'https://zh.annas-archive.org/search?index=&page=1&sort=&q=%%%',
    label: '书籍搜索-安娜的档案',
  },
  {
    value: 'https://www.pdfdrive.com/search?pagecount=&pubyear=&searchin=&em=&q=%%%',
    label: '书籍搜索-pdfDrive',
  },
];
const engines3 = useLocalStorage<{ value: string; label: string }[]>('custom-engines', []);
</script>

<style scoped>
@media screen and (min-width: 430px) {
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;

    .n-transfer {
      width: 300px;
    }
  }
}
@media screen and (max-width: 430px) {
  .container {
    padding: 20px;
    height: 100vh;

    .n-transfer {
      width: 100%;
    }
  }
}
</style>
