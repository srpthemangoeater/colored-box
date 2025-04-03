<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const colorList = ref([
  { color: '#b8f2ff' },
  { color: '#558be0' },
  { color: 'purple' },
  { color: '#021433' }
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
      <button class="colored-box" :style="{ backgroundColor: selectedColor }" @click.stop="toggleColorSelect"></button>
      <h1>Space & Winter</h1>
      <h3>Sleek and Modern</h3>
    </div>

    <div v-if="showColorSelect" class="color-select box">
      <h3>Select Color</h3>
      <div class="color-list">
        <button v-for="color in colorList" :key="color.color" @click="selectedColor = color.color" class="color-each"
          :style="{ backgroundColor: color.color }">
        </button>
      </div>
    </div>
  </div>
</template>

<style lang="css">
.page-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;
}

.box {
  background: #FFFFFF;
  box-shadow: 0px 10px 0px #0000003c;
  border-radius: 1rem;
  color: black !important;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 1.5rem 2rem;
  gap: 5px;

  width: 100%;
  max-width: 1000px;
}

.colored-box {
  border-radius: 1rem;
  width: 100%;
  aspect-ratio: 1 / 1;
  border: none;
}

.colored-box:focus {
  outline: red 2px solid;
}

.color-select .color-list {
  display: flex;
  flex-direction: row;
  gap: 1rem;
}

.color-each {
  border-radius: 0.5rem;
  width: 40px;
  aspect-ratio: 1 / 1;
  border: none;
}

.color-each:focus {
  outline: 2px solid red;
}
</style>
