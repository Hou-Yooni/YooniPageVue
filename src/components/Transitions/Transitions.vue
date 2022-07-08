<template>
  <div
    class="bg-gradient-to-br from-[#e1ddd7] to-{#d7b272} min-h-screen flex items-center justify-center"
  >
    <div
      class="bg-gray-100 py-5 px-7 rounded drop-shadow-[0_25px_25px_rgba(163,133,4,0.1)] transition duration-300 ease-in-out hover:shadow-xl transform hover:scale-125 text-3xl relative"
      style="min-height: 4.5rem; min-width: 400px"
    >
      <transition name="slide-fade">
        <div
          :key="message.value"
          class="absolute w-full left-0 text-2xl text-center font-semibold text-emerald-700"
          style="margin: auto"
        >
          {{ message.value }}
        </div>
      </transition>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";

const MESSAGES: { value: string; interval?: number }[] = [
  {
    value: "Hello I'm Yooni",
  },
  {
    value: "I'm a Engineer",
  },
  {
    value: "I'm a UI/UX Desinger",
  },
  {
    value: "I'm a Graphic Desinger",
  },
  {
    value: "Are you interested in me?",
  },
  {
    value: "Let's start !",
    interval: 6000,
  },
];

type MsgProvider = {
  value?: string;
  interval?: number;
};

const counter = ref<number>(0);
const message = ref<MsgProvider>({});

const changeMessages = () => {
  message.value = MESSAGES[counter.value % MESSAGES.length];
  counter.value++;
  console.log(message.value.interval);
  setTimeout(changeMessages, message.value.interval || 2000);
};

onMounted(() => {
  changeMessages();
});
</script>

<style lang="scss" scoped>
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.7s ease;
}

.slide-fade-enter-from {
  transform: translateY(-50px);
  opacity: 0;
}

.slide-fade-leave-to {
  transform: translateY(30px) scale(0.9);
  opacity: 0;
}
</style>
