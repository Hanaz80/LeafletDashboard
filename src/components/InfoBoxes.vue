<template>
  <div class="card-container">
    <button @click="toggleCards" class="btn toggle-button">
      <i :class="showCards ? 'bi bi-dash-lg' : 'bi bi-plus-lg'" id="item"></i>
    </button>
    
    <div v-for="item in displayedItems" :key="item.id" 
         :class="['card', { 'clicked-card': clickedItemId === item.id }]" 
         @click="handleCardClick(item)">
      <div class="card-body">
        <div class="top-section">
          <span class="three-dots">⋮</span> 
          <p class="card-text">{{ item.status }}</p>
        </div>
        <div class="status-container">
          <div :class="['status-dot', { clicked: clickedItemId === item.id }]" :style="{ backgroundColor: item.color }"></div>
          <h5 class="card-title">{{ item.id }}</h5>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed, defineEmits } from 'vue';
import axios from 'axios';

const items = ref([]);
const showCards = ref(false);
const limit = 6;
const clickedItemId = ref(null); 
const emit = defineEmits();

const toggleCards = () => {
  showCards.value = !showCards.value;
};

const handleCardClick = (item) => {
  clickedItemId.value = item.id; 
  emit('status-selected', item.status); 
};

onMounted(async () => {
  try {
    const response = await axios.get('/scooters.json');
    items.value = response.data;
  } catch (error) {
    console.error('خطا در بارگذاری داده‌ها:', error);
  }
});

const displayedItems = computed(() => 
  showCards.value || items.value.length <= limit ? items.value : items.value.slice(0, limit)
);
</script>

<style scoped lang="scss">
$card-bg-color: white;
$shadow-color: rgba(200, 200, 200, 0.5);
$clicked-shadow: rgba(188, 178, 178, 0.7);
$card-width: 15%;
$dot-size: 12px;
$clicked-border-color: hsl(178.9, 96.6%, 46.3%);

.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  margin-right: 220px;
  cursor: pointer;
}

.card {
  width: $card-width;
  margin: 5px;
  box-sizing: border-box;
  background-color: $card-bg-color;
  border: none;
  box-shadow: 0 4px 8px $shadow-color;
  border-radius: 10px;
  position: relative;
  transition: border 0.3s ease;
}

.clicked-card {
  border: 2px solid $clicked-border-color; 
}

.toggle-button {
  width: 20px;
  margin: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: $card-bg-color;
  border: none;
  box-shadow: 0 2px 4px $shadow-color;
  cursor: pointer;
}

.top-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.status-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
}

.status-dot {
  width: $dot-size;
  height: $dot-size;
  border-radius: 50%;
  box-shadow: none;
}

.status-dot.clicked {
  box-shadow: 0 0 15px 5px $clicked-shadow;
}

.three-dots {
  cursor: pointer;
}
</style>
