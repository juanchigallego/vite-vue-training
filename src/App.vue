<script setup lang="ts">
import { onMounted, onUnmounted, ref } from "vue";
import PrototypeTitle from "./components/PrototypeTitle.vue";
import PlaybookCard from "./components/PlaybookCard.vue";
import { DtButton, DtStack } from "@dialpad/dialtone/vue3";

const className = "dialtone-theme-dark";
const task1 = ref(false);
const task2 = ref(false);
const task3 = ref(false);

onMounted(() => {
  document.body.classList.add(className);
});

onUnmounted(() => {
  document.body.classList.remove(className);
});
</script>

<template>
  <dt-stack class="d-h100vh">
    <prototype-title class="d-p16 d-bgc-primary" title="Playbook" />
    <div class="d-d-flex d-jc-center d-py32 d-fl-grow1">
      <dt-stack class="
        d-ba
        d-bc-default
        d-of-hidden
        d-bar8
        d-d-inline-block
        d-bgc-primary
        d-bs-sm">
        <div>
          <img class="slice slice--dark" src="./assets/topbar--dark.png" alt="">
          <img class="slice slice--light" src="./assets/topbar--light.png" alt="">
        </div>
        <dt-stack direction="row" class="d-ai-flex-start">
          <div>
            <img class="slice slice--dark" src="./assets/leftbar--dark.png" alt="">
            <img class="slice slice--light" src="./assets/leftbar--light.png" alt="">
          </div>
          <div>
            <img class="slice slice--dark" src="./assets/conversation-view--dark.png" alt="">
            <img class="slice slice--light" src="./assets/conversation-view--light.png" alt="">
          </div>
          <div class="playbook-column d-bl d-bc-subtle d-as-stretch">
            <div>
              <img class="slice slice--dark" src="./assets/rightbar-playbook--dark.png" alt="">
              <img class="slice slice--light" src="./assets/rightbar-playbook--light.png" alt="">
            </div>
            <dt-stack gap="300" class="d-p8">
              <playbook-card
                title="Budget"
                question="This animation is using a CSS sprite"
                summary="The customer says they have $24,000 allocated to this effort and they do not see requirements taking them over the budget."
                :checked-by-a-i="task1"
                @update:checked-by-a-i="task1 = $event"
                check-animation="css" />
              <playbook-card
                title="Authority"
                question="This Playbook card is animated using Lottiefiles"
                summary="The customer says they have $24,000 allocated to this effort and they do not see requirements taking them over the budget."
                :checked-by-a-i="task2"
                @update:checked-by-a-i="task2 = $event"
                check-animation="lottie" />
              <playbook-card
                title="Need"
                question="This checkbox is animated with GSAP"
                summary="The customer says they have $24,000 allocated to this effort and they do not see requirements taking them over the budget."
                :checked-by-a-i="task3"
                @update:checked-by-a-i="task3 = $event"
                check-animation="gsap" />
            </dt-stack>
          </div>
          <div>
            <img class="slice slice--dark" src="./assets/skinnybar--dark.png" alt="">
            <img class="slice slice--light" src="./assets/skinnybar--light.png" alt="">
          </div>
        </dt-stack>
        <div>
          <img class="slice slice--dark" src="./assets/callbar--dark.png" alt="">
          <img class="slice slice--light" src="./assets/callbar--light.png" alt="">
        </div>
      </dt-stack>
    </div>
    <dt-stack direction="row" gap="500" class="d-p16 d-bgc-primary d-jc-center">
      <dt-button importance="outlined" kind="muted" @click="task1 = !task1">Complete Budget task</dt-button>
      <dt-button importance="outlined" kind="muted" @click="task2 = !task2">Complete Authority task</dt-button>
      <dt-button importance="outlined" kind="muted" @click="task3 = !task3">Complete Need task</dt-button>
    </dt-stack>
  </dt-stack>
</template>

<style lang="less">
body {
  background-color: var(--dt-color-surface-bold);
}

.playbook-column {
  width: 361px;
  /* with of Playbook column's image slices */
}

.slice {
  display: none;
  pointer-events: none;
  user-select: none;

  &--light {
    .dialtone-theme-light & {
      display: block;
    }
  }

  &--dark {
    .dialtone-theme-dark & {
      display: block;
    }
  }
}
</style>
