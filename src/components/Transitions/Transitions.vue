<template>
  <div
    class="bg-gradient-to-br from-[#e1ddd7] to-{#d7b272} min-h-screen flex items-center justify-center relative transition-all duration-700 opacity-1"
    :class="[...clickBgStyle]"
  >
    <div
      class="bgBtnHover bg-gray-100 py-5 px-7 h-20 absolute overflow-hidden rounded drop-shadow-[0_25px_25px_rgba(163,133,4,0.1)] transition-all duration-700 ease-in-out transform w-96 hover:rounded-[999rem] hover:h-[10rem] hover:w-[10rem] hover:transition-all hover:duration-700 hover:shadow-none text-3xl cursor-pointer group top-2/4 right-2/4 translate-y-[-50%] translate-x-[50%]"
      :class="[[...clickCircleStyle], { bgBtnFixed: isDestroyElement }]"
      @mouseover="hoverStatus = true"
      @mouseleave="hoverStatus = false"
      @click="enterIndexHandler"
    >
      <transition name="slide-fade" v-if="!isDestroyElement">
        <div
          :key="message.value"
          class="absolute w-full pt-1 left-0 text-2xl text-center font-semibold text-emerald-700 duration-75 group-hover:opacity-0 hover:transition-all hover:duration-75"
          style="margin: auto"
        >
          {{ message.value }}
        </div>
      </transition>
      <p
        v-if="hoverStatus && !isDestroyElement"
        class="text-2xl text-emerald-700 font-semibold absolute top-2/4 left-2/4 translate-y-[-50%] translate-x-[-50%]"
      >
        Click
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, nextTick } from "vue";

/* props */
const props = defineProps({
  isDestroy: {
    type: Boolean,
    required: false,
  },
});

/* emits */
const emit = defineEmits(["update:isDestroy"]);

/* messages */
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

/* type */
type MsgProvider = {
  value?: string;
  interval?: number;
};

/* Change mssages */
const counter = ref<number>(0);
const message = ref<MsgProvider>({});

const changeMessages = () => {
  message.value = MESSAGES[counter.value % MESSAGES.length];
  counter.value++;
  setTimeout(changeMessages, message.value.interval || 2000);
};

onMounted(() => {
  changeMessages();
});

/* Hoever mssages */
const hoverStatus = ref<boolean>(false);

/* Enter Index */
const clickCircleStyle = ref<string[]>([]);
const clickBgStyle = ref<Array<string>>([]);
const isDestroyElement = ref<boolean>(false);
const enterIndexHandler = () => {
  isDestroyElement.value = true;

  clickCircleStyle.value = [
    "w-screen",
    "h-screen",
    "hover:h-screen",
    "hover:w-screen",
    "hover:rounded-[0rem]",
  ];

  setTimeout(() => {
    clickCircleStyle.value.push(
      "absolute",
      "top-[40px]",
      "right-[55px]",
      "w-4",
      "h-4",
      "hover:w-4",
      "hover:h-4",
      "hover:rounded-full",
      "rounded-full"
    );
  }, 1700);
  setTimeout(() => {
    clickBgStyle.value = ["opacity-0"];
  }, 3000);
  setTimeout(() => {
    emit("update:isDestroy", true);
  }, 4300);
};
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

@mixin transBg($color) {
  animation: zigzag 1s linear infinite;
  background: linear-gradient(
        135deg,
        rgba($color, 0.25) 0.25em,
        transparent 0.25em
      ) -0.5em 0,
    linear-gradient(225deg, rgba($color, 0.25) 0.25em, transparent 0.25em) -0.5em
      0,
    linear-gradient(315deg, rgba($color, 0.25) 0.25em, transparent 0.25em) 0 0,
    linear-gradient(45deg, rgba($color, 0.25) 0.25em, transparent 0.25em) 0 0;
  background-size: 0.75em 0.75em;
  color: adjust-hue($color, 180);
}

.bgBtnHover {
  $color: #eea163;
  color: $color;

  &:hover {
    @include transBg($color);
  }
}

.bgBtnFixed {
  $color: #eea163;
  color: $color;
  @include transBg($color);
}

@keyframes zigzag {
  100% {
    background-position: 1em 0, 1em 0, -0.75em 0, -0.75em 0;
  }
}
</style>
