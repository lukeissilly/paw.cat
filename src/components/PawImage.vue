<template>
  <div class="flex flex-col items-center justify-center min-h-screen">
    <img
        src="/paw.png"
        @click="handleClick"
        class="w-64 h-64 cursor-pointer transition-transform transform hover:scale-110"
        alt="Clickable paw image"
    />
    <p class="mt-4 text-2xl font-semibold text-gray-100 dark:text-gray-100">
      Paw Count:
      <span class="text-indigo-600 dark:text-indigo-500">{{ count }}</span>
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';

const clickSound = new Audio('/meow.mp3');

const count = ref(0);

onMounted(() => {
  const savedCount = localStorage.getItem('pawClickCount');
  if (savedCount !== null) {
    count.value = parseInt(savedCount, 10);
  }
});

watch(count, (newValue) => {
  localStorage.setItem('pawClickCount', newValue);
});

const handleClick = () => {
  count.value++;
  playSound();
};

const playSound = () => {
  clickSound.currentTime = 0;
  clickSound.play();
};
</script>
