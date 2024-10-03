<template>
  <div class="card">
    <h6 class="card-title">لیست اسکوتر ها</h6>
    <div class="card-body">
      <table class="table">
        <thead>
          <tr>
            <th ></th>
            <th >کد کاربر</th>
            <th >کد اسکوتر</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in items" :key="item.id">
            <td><i class="bi bi-three-dots-vertical"></i></td>
            <td class="text-right">{{ item.number }}</td> 
            <td class="text-right">{{ item.code }}</td> 
          </tr>
        </tbody>
      </table>
    </div>
    <nav aria-label="Page navigation example" class="text-center mt-2"> 
      <ul class="pagination">
        <li class="page-item">
          <a class="page-link" href="#" aria-label="Previous">
            <span aria-hidden="true">&laquo;</span>
          </a>
        </li>
        <li class="page-item"><a class="page-link" href="#">1</a></li>
        <li class="page-item"><a class="page-link" href="#">2</a></li>
        <li class="page-item"><a class="page-link" href="#">3</a></li>
        <li class="page-item">
          <a class="page-link" href="#" aria-label="Next">
            <span aria-hidden="true">&raquo;</span>
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const items = ref([]);

onMounted(async () => {
  try {
    const response = await axios.get('/scooters.json'); 
    items.value = response.data;
  } catch (error) {
    console.error('Error loading data:', error);
  }
});
</script>

<style scoped>
 
.card {
  border: none; 
  box-shadow: 0 4px 8px rgba(200, 200, 200, 0.5);
  border-radius: 10px; 
  background-color: white; 
}

.card-title {
  text-align: right; 
  margin-bottom: 10px;  
  border-bottom: 2px solid #ccc;
  padding: 25px; 
}


.card-body {
  padding: 0;
  width: 300px;
}

.table {
  width: 100%;
  margin: 0;
  border-collapse: collapse; 
  background-color: white; 
}

.table th, .table td {
  padding: 8px; 
  text-align: right; 
  background-color: white; 
  color: #828b98;
}

.pagination {
  justify-content: center;
}

.page-link {
  color: #333; 
}

</style>
