<template>
  <div class="flex space-x-2 items-center px-5">
    <div class="text-gray-500 text-xs" v-if="showNextModeLabel">
      Change to {{ nextMode }}
    </div>
    <button
      @click="toggleMode"
      @mouseenter="showNextModeLabel = true"
      @mouseleave="showNextModeLabel = false"
      class="bg-yellow-300 p-9 md:p-3 rounded-[50%]"
      :class="{ darkToggle: !isDark }"
    ></button>
  </div>
</template>

<script setup>
const colorMode = useColorMode();
const showNextModeLabel = ref(false);
const isDark = ref(true);

const modes = ["light", "dark"];

const nextMode = computed(() => {
  const currentModeIndex = modes.indexOf(colorMode.preference);
  let nextModeIndex = null;
  if (currentModeIndex + 1 === modes.length) {
    nextModeIndex = 0;
  } else {
    nextModeIndex = currentModeIndex + 1;
  }
  return modes[nextModeIndex];
});

const toggleMode = computed(() => {
  colorMode.preference = nextMode.value;
  isDark.value = !isDark.value;
});
</script>
<style>
.darkToggle {
  @apply bg-gray-800 text-gray-300;
}
</style>
