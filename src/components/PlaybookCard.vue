<script setup lang="ts">
import { computed, ref, watch, defineEmits, onMounted, nextTick } from "vue";
import { DtStack, DtCheckbox, DtCollapsible, DtButton, DtSkeleton, DtIcon } from "@dialpad/dialtone/vue3";
import SparkleIcon from "./SparkleIcon.vue";
import { DotLottieVue } from '@lottiefiles/dotlottie-vue';
import { gsap } from "gsap";

const checkedByAgent = ref(false);
const id = computed(() => props.title?.replace(/ /g, "-").toLowerCase());
const isOpen = ref(true);
const showSummary = ref(false);
const showSummarySkeleton = ref(true);
const showSummaryContent = ref(false);
const showQuestionsToggle = ref(false);
const playerRef = ref<any>(null);

type AnimationType = 'lottie' | 'css' | 'gsap';

const sparksContainer = ref<HTMLElement | null>(null);

onMounted(() => {
  if (props.checkAnimation === 'gsap') {
    nextTick(() => {
      if (sparksContainer.value) {
        createSparks(24, sparksContainer.value);
        gsap.set(sparksContainer.value, { autoAlpha: 0 });
      } else {
        console.error('Sparks container not found');
      }
    });
  }
});

const props = defineProps({
  title: String,
  question: String,
  summary: String,
  checkedByAI: Boolean,
  checkAnimation: {
    type: String as () => AnimationType,
    default: 'css',
    validator: (value: string): boolean => ['lottie', 'css', 'gsap'].includes(value)
  }
});

const emits = defineEmits(["update:checkedByAI"]);

const toggleTaskCompletion = () => {
  checkedByAgent.value = !checkedByAgent.value;
  if (props.checkedByAI) {
    emits("update:checkedByAI", false);
    checkedByAgent.value = false;
  }
}

const handleAnimationEnd = () => {
  showSummary.value = true;
  showQuestionsToggle.value = true;
  isOpen.value = false;
  setTimeout(() => {
    showSummarySkeleton.value = false;
    showSummaryContent.value = true;
  }, 2500);
};

watch(() => checkedByAgent.value, (newValue) => {
  if (newValue === true) {
    isOpen.value = false;
  } else {
    isOpen.value = true;
  }
})

// Reset the state when unchecking by AI
watch(() => props.checkedByAI, (newValue) => {
  if (newValue === false) {
    showSummary.value = false;
    showSummarySkeleton.value = true;
    showSummaryContent.value = false;
    showQuestionsToggle.value = false;
    isOpen.value = true;
  }
  if (newValue === true && playerRef.value) {
    const dotLottie = playerRef.value.getDotLottieInstance();
    dotLottie.play();
  }
  if (newValue === true && props.checkAnimation === "gsap") {
    playGsapAnimation();
  }
});

// GSAP animation
function createSparks(numberOfSparks: number, container: HTMLElement | null) {
  if (!container) return;

  for (let i = 0; i < numberOfSparks; i++) {
    let spark = document.createElementNS("http://www.w3.org/2000/svg", "path");
    spark.setAttribute(
      "d",
      "M1.86328 0.103888C2.08176 0.128789 2.50638 1.31122 2.50638 1.31122C2.50638 1.31122 3.59592 1.69832 3.59224 2.03561C3.58857 2.37291 2.49061 2.76001 2.49061 2.76001C2.49061 2.76001 2.12883 3.96734 1.82121 3.96734C1.51359 3.96734 1.20709 2.76001 1.20709 2.76001C1.20709 2.76001 0.0880284 2.42271 0.0922434 2.03561C0.0964584 1.64851 1.22287 1.31122 1.22287 1.31122C1.22287 1.31122 1.6448 0.0789868 1.86328 0.103888Z"
    );
    spark.setAttribute("class", "spark");
    container.appendChild(spark);
  }
}

function playGsapAnimation() {
  if (!sparksContainer.value) return;

  gsap.set(sparksContainer.value, { autoAlpha: 1 });
  const sparks = sparksContainer.value.querySelectorAll(".spark");

  sparks.forEach((spark: Element) => {
    gsap.set(spark, { autoAlpha: 1, scale: 1, x: 8, y: 8 });
    const angle = Math.random() * 360;
    const distance = gsap.utils.random(24, 32, 1);
    const x = Math.cos((angle * Math.PI) / 180) * distance;
    const y = Math.sin((angle * Math.PI) / 180) * distance;

    gsap
      .timeline({ delay: 0.5 })
      .fromTo(
        spark,
        { autoAlpha: 0, rotation: 0 },
        {
          autoAlpha: 1,
          scale: "random(2, 2.5)",
          x: x,
          y: y,
          rotation: "random(0, 10)",
          duration: 1,
          ease: "power4.out"
        }
      )
      .to(spark, { autoAlpha: 0, duration: 0.5 }, "-=0.5");
  });
};
</script>

<template>
  <div class="dt-card-ai" :data-checked-by-agent="checkedByAgent"
    :data-checked-by-ai="props.checkedByAI ? 'true' : 'false'" @animationend="handleAnimationEnd">
    <div v-if="checkAnimation === 'css'" class="check-css">
      <img src="https://i.imgur.com/gnhkNJL.png" aria-hidden="true" />
    </div>
    <div v-else-if="checkAnimation === 'lottie'" class="d-ps-absolute d-t4 d-l0 d-pe-none">
      <DotLottieVue style="height: 32px; width: 32px" :speed=".5" ref="playerRef"
        src="https://lottie.host/cae6a34c-be47-4745-a262-355a82639802/hJJCgT4iWv.lottie" />
    </div>
    <div v-else class="check-gsap d-fc-primary-inverted" data-active="false">
      <dt-icon name="check" size="200" v-if="props.checkedByAI" />
      <svg class="sparks" ref="sparksContainer"></svg>
    </div>
    <dt-checkbox aria-label="Complete task" :name="`complete-${id}-task`" :id="`complete-${id}-task`"
      :checked="checkedByAgent" @click="toggleTaskCompletion" />
    <dt-stack gap="300" class="d-ai-flex-start">
      <dt-stack direction="row" gap="300">
        <label :for="`complete-${id}-task`" class="d-headline--md">{{ props.title }}</label>
        <sparkle-icon />
      </dt-stack>
      <p class="d-body--sm-compact d-fc-primary">{{ props.question }}</p>
      <dt-collapsible :open="isOpen">
        <template #content>
          <ul class="d-lst-disc d-pl16">
            <li class="d-body--md-compact d-fc-primary d-lst-disc">What is your allocated budget for this project or
              solution?</li>
            <li class="d-body--md-compact d-fc-primary d-lst-disc">Have you considered any financial restraints?</li>
          </ul>
        </template>
        <template #anchor>
          <dt-button class="d-link--muted d-body--sm-compact" link @click="isOpen = !isOpen">
            {{ isOpen ? 'Hide questions' : 'Show questions' }}
          </dt-button>
        </template>
      </dt-collapsible>
      <dt-stack v-if="showSummary" class="d-w100p">
        <dt-skeleton v-if="showSummarySkeleton" aria-label="Generating summary" :paragraphOption="{
          rows: 4,
          width: ['30%', '100%', '100%', '40%']
        }" />
        <dt-stack v-if="showSummaryContent">
          <h4 class="d-headline--sm d-fc-primary">Answer summary:</h4>
          <p class="d-body--sm d-fc-primary">{{ props.summary }}</p>
        </dt-stack>
      </dt-stack>
    </dt-stack>
  </div>
</template>
