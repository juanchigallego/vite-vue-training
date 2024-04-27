<script setup lang="ts">
import { onMounted, onUnmounted } from "vue";
import PlaybookPanel from "./components/PlaybookPanel.vue";
import AppHeader from "./components/AppHeader.vue";
import { DtRootLayout, DtAvatar, DtStack } from "@dialpad/dialtone/vue3";

const className = "dialtone-theme-dark";

onMounted(() => {
  document.body.classList.add(className);
});

onUnmounted(() => {
  document.body.classList.remove(className);
});
</script>

<template>
  <dt-root-layout
    header-sticky="true"
    headerClass="d-d-flex d-ai-center d-gg16 d-p12 d-bb d-bc-default"
    sidebarClass="d-d-flex d-ai-center d-jc-center d-gg16 d-p12 d-br d-bc-default d-bgc-secondary d-w164"
    contentClass="chat__wrapper"
  >
    <template #header>
      <app-header />
    </template>
    <template #sidebar>
      <p class="d-body--sm d-fc-tertiary">Sidebar</p>
    </template>
    <template #default>
      <dt-stack direction="row" class="chat__header d-px16 d-py6 d-br d-bb d-bc-default">
        <dt-stack direction="row" gap="400">
          <dt-avatar
            full-name="Darth Vader"
            size="md"
            color="1000"
            presence="active"
          />
          <dt-stack>
            <h2 class="d-font-headline--lg-compact">Darth Vader</h2>
            <p class="d-font-body--sm-compact">Mobile: (919) 123-4567</p>
          </dt-stack>
        </dt-stack>
      </dt-stack>
      <div class="chat__container d-br d-bb d-bc-default"></div>
      <div class="chat__message-box d-p12 d-br d-bc-default">
        <p class="d-body--md d-fc-placeholder">New message</p>
      </div>
      <div class="chat__sidebar d-bgc-secondary">
        <playbook-panel />
      </div>
    </template>
  </dt-root-layout>
</template>

<style scoped>
  h2 {
    line-height: 100%;
  }
</style>
