<template>
  <div class="relative">
    <div
      v-if="isDestroy"
      class="absolute top-[20px] right-[20px] transition-all duration-700 opacity-1"
      :class="['isDestroy' ? 'opacity-1' : 'opacity-0']"
    >
      <ToggleButton />
    </div>
    <Transitions v-if="!isDestroy" v-model:isDestroy="isDestroy" />
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from "vue";
import ToggleButton from "@/components/ToggleButton.vue";
import Transitions from "@/components/Transitions/Transitions.vue";

const isDestroy = ref<boolean>(false);

watch(isDestroy, (val) => {
  console.log(val);
});
</script>
