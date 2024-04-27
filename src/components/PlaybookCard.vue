<script setup lang="ts">
import { ref, watch } from "vue";
import { DtIcon, DtStack, DtCheckbox } from "@dialpad/dialtone/vue3";
import { DotLottieVue } from '@lottiefiles/dotlottie-vue'

const checkedByUser = ref(false);

const props = defineProps({
  title: String,
  question: String,
  summary: String,
  checkedByAI: Boolean,
});

const playerRef = ref<any>(null);

watch(() => props.checkedByAI, (newVal) => {
  if (newVal === true && playerRef.value) {
    const dotLottie = playerRef.value.getDotLottieInstance();
    dotLottie.play();
  }
});
</script>

<template>
  <div class="dt-card-ai" :data-checked-by-user="checkedByUser" :data-checked-by-ai="props.checkedByAI ? 'true' : 'false'">
    <dt-checkbox aria-label="Complete task" name="Complete task" value="checkedByUser" v-model="checkedByUser" />
    <div class="d-ps-absolute d-t4 d-l0 d-pe-none">
        <DotLottieVue style="height: 32px; width: 32px" :speed=".5" ref="playerRef" src="https://lottie.host/cae6a34c-be47-4745-a262-355a82639802/hJJCgT4iWv.lottie" />
    </div>
    <dt-stack gap="300">
      <dt-stack direction="row" gap="400">
        <h3 class="d-headline--md">{{ props.title }}</h3>
        <dt-icon name="sparkle" size="500" />
      </dt-stack>
      <p class="d-body--md-compact d-fc-tertiary">{{ props.question }}</p>
      <dt-stack>
        <h4 class="d-headline--sm d-fc-primary">Answer summary:</h4>
        <p class="d-body--sm d-fc-primary">{{ props.summary }}</p>
      </dt-stack>
    </dt-stack>
  </div>
</template>
