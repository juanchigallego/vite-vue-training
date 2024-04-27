<script setup lang="ts">
import {
  DtIcon,
  DtAvatar,
  DtButton,
  DtInput,
  DtStack,
} from "@dialpad/dialtone/vue3";

const toggleTheme = () => {
  document.body.classList.toggle("dialtone-theme-light");
  document.body.classList.toggle("dialtone-theme-dark");
};
</script>

<template>
  <dt-icon name="brand-dialpad" size="600" />
  <dt-stack direction="row">
    <dt-button circle importance="clear">
      <template #icon>
        <dt-icon name="phone" size="300" />
      </template>
    </dt-button>
    <dt-button circle importance="clear">
      <template #icon>
        <dt-icon name="message" size="300" />
      </template>
    </dt-button>
    <dt-button circle importance="clear">
      <template #icon>
        <dt-icon name="video" size="300" />
      </template>
    </dt-button>
  </dt-stack>
  <dt-stack direction="row" gap="400" class="d-jc-center d-fl1">
    <dt-stack direction="row">
      <dt-button circle importance="clear">
        <template #icon>
          <dt-icon name="arrow-left" size="300" />
        </template>
      </dt-button>
      <dt-button circle importance="clear" disabled>
        <template #icon>
          <dt-icon name="arrow-right" size="300" />
        </template>
      </dt-button>
      <dt-button circle importance="clear">
        <template #icon>
          <dt-icon name="refresh" size="300" />
        </template>
      </dt-button>
    </dt-stack>
    <dt-input type="search" placeholder="Search Dialpad">
      <template #leftIcon>
        <dt-icon name="search" size="300" />
      </template>
    </dt-input>
  </dt-stack>
  <dt-stack direction="row">
    <dt-button circle importance="clear">
      <template #icon>
        <dt-icon name="settings" size="300" />
      </template>
    </dt-button>
    <dt-button circle importance="clear">
      <template #icon>
        <dt-icon name="calendar" size="300" />
      </template>
    </dt-button>
    <dt-avatar
      full-name="Juan Manuel Gallego"
      size="md"
      color="1000"
      presence="active"
    />
    <dt-button circle importance="clear">
      <template #icon>
        <dt-icon name="more-vertical" size="300" />
      </template>
    </dt-button>
    <dt-button @click="toggleTheme">
      <template #icon>
        <dt-icon name="circle-half-filled" size="300" />
      </template>
      <template #default>Toggle theme</template>
    </dt-button>
  </dt-stack>
</template>
