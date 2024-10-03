<template>
  <div class="body">
    <Table class="me-4" />
    <div id="map" class="map"></div>
  </div>
</template>

<script setup>
import Table from './Table.vue';
import { onMounted, ref, watch } from 'vue';
import L from 'leaflet';
import axios from 'axios';

const props = defineProps({
  selectedStatus: String,
});

const map = ref(null);
const markers = ref([]);
const scootersData = ref([]); // ذخیره داده‌ها در حافظه

const loadScooters = async () => {
  try {
    const response = await axios.get('/scooters.json');
    scootersData.value = response.data; // ذخیره داده‌ها برای دسترسی بعدی
  } catch (error) {
    console.error('Error loading scooters:', error);
  }
};

const updateMap = () => {
  // پاک کردن نشانگرهای قبلی از نقشه
  markers.value.forEach(marker => marker.remove());
  markers.value = [];

  // افزودن نشانگرهای جدید بر اساس وضعیت انتخاب شده
  scootersData.value
    .filter(scooter => !props.selectedStatus || scooter.status === props.selectedStatus)
    .forEach(scooter => {
      const marker = L.marker([scooter.latitude, scooter.longitude], {
        icon: L.divIcon({
          className: 'scooter-icon',
          html: `<i class="bi bi-dot" style="color:${scooter.color}; font-size:50px;"></i>`,
        }),
      });
      marker.addTo(map.value);
      markers.value.push(marker);

      // افزودن رویداد کلیک به نشانگر
      marker.on('click', () => {
        const popupContent = `
          <div class="text-center">
            <i class="bi bi-scooter j" style="font-size:50px"></i></li>
            <p > ${scooter.code}</p>
            <p> وضعیت: ${scooter.status} </p>
          </div>
        `;
        marker.bindPopup(popupContent).openPopup();
      });
    });
};

onMounted(async () => {
  // مقداردهی اولیه نقشه
  map.value = L.map('map').setView([35.6892, 51.3890], 13);
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
  }).addTo(map.value);

  // بارگذاری اولیه اسکوترها و به‌روزرسانی نقشه
  await loadScooters();
  updateMap();
});

watch(() => props.selectedStatus, () => {
  updateMap();
});
</script>

<style scoped>
.body {
  display: flex;
  width: 100%;
  margin: 10px;
  position: relative; 
}

.map {
  height: 100vh; 
  width: 60%; 
  box-shadow: 0 4px 8px rgba(200, 200, 200, 0.5);
  margin-left: 10px; 
  overflow: hidden; 
  border-radius: 15px; 
}

.table {
  height: 100%; 
  width: 35%; 
  overflow-y: auto; 
}
</style>
