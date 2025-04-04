<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const colorList = ref([
  { color: '#CBEFFF' },
  { color: '#1A64FC' },
  { color: '#6700F0' },
  { color: '#181448' }
]);

const selectedColor = ref('');
const showColorSelect = ref(false);

const toggleColorSelect = () => {
  showColorSelect.value = !showColorSelect.value;
};

const closeColorSelect = (event: Event) => {
  if (!(event.target as HTMLElement).closest('.box')) {
    showColorSelect.value = false;
  }
};

onMounted(() => {
  document.addEventListener('click', closeColorSelect);
});

onUnmounted(() => {
  document.removeEventListener('click', closeColorSelect);
});
</script>

<template>
  <div class="page-container">
    <div class="box">
      <button class="colored-box" :class="{ 'red-outline': showColorSelect }"
        :style="{ backgroundColor: selectedColor }" @click="toggleColorSelect"></button>
      <div style="width: 100%;">
        <h1>Space Winter</h1>
        <h2>Modern & Sleek</h2>
      </div>
    </div>

    <div v-if="showColorSelect" class="color-select box">
      <h3>Select Color :</h3>
      <div class="color-list">
        <button v-for="color in colorList" :key="color.color" @click="selectedColor = color.color" class="color-each"
          :style="{ backgroundColor: color.color }">
        </button>
      </div>
    </div>
  </div>
</template>

<style lang="css">
button:hover {
  cursor: pointer;
}

.page-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  width: 100%;
}

.box {
  background: #FFFFFF;
  box-shadow: 0px 6px 0px #0000003c;
  border-radius: 1rem;
  color: black !important;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 1.3rem 1.3rem;
  gap: 10px;

  width: 100%;
  max-width: 1000px;
}


.colored-box {
  border-radius: 0.5rem;
  width: 100%;
  aspect-ratio: 1 / 1;
  border: none;
}

.color-list {
  width: 100%;
}

.color-list .colored-box:focus {
  outline: red 1px solid;
}

.red-outline {
  outline: red 1px solid;
}

.color-select .color-list {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  justify-content: space-between;
}

.color-each {
  border-radius: 0.5rem;
  width: 60px;
  aspect-ratio: 1 / 1;
  border: none;
}

.color-each:focus {
  border: 1px solid red;
}
</style>
