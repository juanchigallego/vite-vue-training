<script setup lang="ts">
import { ref } from "vue";
import PlaybookCard from "./PlaybookCard.vue";
import { DtStack, DtButton, DtIcon } from "@dialpad/dialtone/vue3";

const checkedByAI = ref(false);

const toggleCompleted = () => {
  checkedByAI.value = !checkedByAI.value;
}
</script>

<template>
  <dt-stack>
    <dt-stack direction="row" class="d-px16 d-py12 d-jc-space-between d-bb d-bc-default">
      <h2 class="font-headline--lg-compact">Playbook</h2>
      <dt-button circle importance="clear">
        <template #icon>
          <dt-icon name="close" size="300" />
        </template>
      </dt-button>
    </dt-stack>
    <dt-stack gap="450" class="d-p12">
      <playbook-card title="Budget" question="Have you identified a budget range for this purchase?"
        summary="Cras mattis consectetur purus sit amet fermentum. Lorem ipsum dolor sit amet, consectetur adipiscing elit." />
      <playbook-card
        title="Shipping"
        question="Are the shipping times and cost adequate?"
        summary="Cras mattis consectetur purus sit amet fermentum. Lorem ipsum dolor sit amet, consectetur adipiscing elit."
        :checkedByAI="checkedByAI"
      />
      <dt-button @click="toggleCompleted">
        <template #default>Complete by AI</template>
      </dt-button>
    </dt-stack>
  </dt-stack>
</template>