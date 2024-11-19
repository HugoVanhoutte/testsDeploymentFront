<script setup lang="ts">
import { onMounted, ref } from 'vue';

const testData = ref<string | object>('');

const test = async (): Promise<void> => {
  try {
    console.log('test');
    const res = await fetch('http://testsdeploiementback-production.up.railway.app/api/route/test', {
      method: 'GET',
      headers: { accept: 'application/json' },
    });
    const data = await res.json();
    if (!res.ok) {
      console.error(res.status, data.message);
    } else {
      console.log(data);
      testData.value = data;
    }
  } catch (error) {
    console.error('Fetch error:', error);
  }
};

onMounted(() => {
  test();
});
</script>

<template>
  <h1>{{ testData.test }}</h1>
</template>

<style scoped lang="scss">
/* Add your styles here */
</style>
