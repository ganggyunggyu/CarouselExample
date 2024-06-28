<template>
  <div class="carousel-container">
    <button class="prev" @click="prevSlide">Prev</button>
    <div class="carousel">
      <div
        class="carousel-item"
        v-for="(item, index) in displayedItems"
        :class="i === currentIndex && 'small'"
        :key="index"
      >
        {{ item }}
      </div>
    </div>
    <button class="next" @click="nextSlide">Next</button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const items = [1, 2, 3];
const currentIndex = ref(0);

const displayedItems = computed(() => {
  const length = items.length;
  return [
    items[(currentIndex.value - 1 + length) % length],
    items[currentIndex.value],
    items[(currentIndex.value + 1) % length],
  ];
});

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % items.length;
};

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + items.length) % items.length;
};
</script>

<style scoped>
.small {
  scale: 0.5;
}
.carousel-container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 50%;
  height: 100vh;
  overflow: scroll;
}

button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 2;
}

.prev {
  left: 10px;
}

.next {
  right: 10px;
}

.carousel {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.carousel-item {
  min-width: 300px;
  height: 400px;
  background-color: red;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 10px;
}
</style>
