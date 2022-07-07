<template>
  <div
    id="app"
    class="bg-gradient-to-br from-purple-900 to-blue-700 min-h-screen flex items-center justify-center"
  >
    <div
      class="bg-gray-100 py-5 px-7 rounded shadow transition duration-300 ease-in-out hover:shadow-xl transform hover:scale-125 text-3xl relative"
      style="min-height: 5rem; min-width: 400px"
    >
      <transition name="slide-fade">
        <div
          :key="message.value"
          class="absolute w-full left-0 text-center font-semibold"
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
    value: "I'm a Desinger",
  },
  {
    value: "I'm a Engineer",
  },
  {
    value: "Fourth Message",
  },
  {
    value: "Longer 5th Message",
    interval: 5000,
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
.body {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #efeae5;
}
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.4s ease;
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
