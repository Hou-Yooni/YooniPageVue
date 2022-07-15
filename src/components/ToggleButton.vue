<template>
  <div
    id="menuToggle"
    class="w-[4.1rem] h-[2.8rem] rounded-full bg-white drop-shadow-[0_4px_2px_rgba(163,133,4,0.1)]"
  ></div>
</template>
<script setup lang="ts"></script>

<style lang="scss" scoped>
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

.menuToggle {
  $color: #eea163;
  color: $color;
  &:hover {
    @include transBg($color);
  }
}
</style>
