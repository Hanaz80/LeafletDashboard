<template>
  <div class="dashboard">
    <Sidebar />
    <div class="main-content">
      <Header />
      <div class="map-section">
        <InfoBoxes @status-selected="status => selectedStatus = status" />
        <MapComponent :selectedStatus="selectedStatus" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Sidebar from './Sidebar.vue';
import Header from './Header.vue';
import InfoBoxes from './InfoBoxes.vue';
import MapComponent from './MapComponent.vue';

const selectedStatus = ref('');
</script>

<style scoped lang="scss">
.dashboard {
  display: flex; 
  padding: 0 20px;
}

.main-content {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.map-section {
  flex: 1; 
}
</style>
