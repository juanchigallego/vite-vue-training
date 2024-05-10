<script setup lang="ts">
  import { defineProps, type PropType } from 'vue';
  import { DtButton, DtIcon, DtStack } from "@dialpad/dialtone/vue3";

  const { title } = defineProps({
    title: {
      type: String as PropType<string>,
      default: 'Dialtone sample'
    }
  });

  const toggleTheme = () => {
    const bodyEl = document.body;
    bodyEl.classList.toggle('dialtone-theme-light');
    bodyEl.classList.toggle('dialtone-theme-dark');
  };
</script>

<template>
  <dt-stack direction="row" class="d-jc-space-between">
    <h1 class="d-headline-extra-large"> {{ title }} </h1>
    <dt-stack direction="row" gap="500">
      <dt-button importance="outlined" size="md" @click="toggleTheme">
        <template #icon>
          <dt-icon name="circle-half-filled" size="300" />
        </template>
      </dt-button>
    </dt-stack>
  </dt-stack>
</template>
<style lang="less">
</style>
