<script setup>
import { onMounted, ref, watch } from 'vue';

const arr = [0, 1, 2, 3, 4, 5];

const curIndex = ref(null);

var intersectionObserver = new IntersectionObserver(function (entries) {
  if (entries[0].intersectionRatio <= 0) return;

  loadItems(10);
  console.log('새 항목 불러옴');
});

const el = document.querySelector('section');

onMounted(() => {
  console.log(el);
});
</script>
<template>
  <main>
    <section>
      <div v-for="e in arr" :key="e">
        {{ e }}
      </div>
    </section>
  </main>
</template>

<style scoped>
main {
  display: flex;
  align-items: center;
  justify-content: center;
}
section {
  width: 50vw;
  display: flex;
  gap: 10px;
  overflow-x: scroll;
  scroll-snap-type: x mandatory;
}
div {
  min-width: 30vw;
  height: 500px;
  background-color: aqua;
  scroll-snap-align: center; /* 스크롤 위치 맞춤 */
}
</style>
