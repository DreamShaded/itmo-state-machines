<script setup>
import { useNav } from "@slidev/client";
import { computed } from "vue";

const nav = useNav();
const currentPage = computed(() => nav.currentPage.value);
const showNumber = computed(() => currentPage.value > 1);
</script>

<template>
  <div class="slidev-layout center">
    <div class="center__container">
      <slot />
    </div>
    <div v-if="showNumber" class="slide-number">
      {{ currentPage }}
    </div>
  </div>
  
</template>


