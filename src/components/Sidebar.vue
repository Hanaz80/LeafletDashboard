<template>
  <div class="sidebar">
    <div class="headerSide">
      <img src="https://imgurl.ir/uploads/k7496_tal.png">
      <h2>تال</h2>
    </div>
    <ul>
      <li>نقشه زنده<i class="bi bi-map"></i></li>
      <li> داشبورد<i class="bi bi-grid-fill"></i></li>
      <li> گزارش‌ها<i class="bi bi-file-earmark-text"></i></li>
      <li> سواری‌ها <i class="bi bi-bicycle"></i></li>
      <li> اسکوتورها<i class="bi bi-scooter"></i></li>
      <li> کاربران <i class="bi bi-person"></i></li>
      <li> پیام‌ها <i class="bi bi-chat-dots"></i></li>
      <li> تنظیمات <i class="bi bi-gear"></i></li>
      <li> مدیریت درآمد<i class="bi bi-cash-stack"></i></li>
      <li> برنامه‌های مالی<i class="bi bi-bar-chart"></i></li>
      <li> مناطق جغرافیایی<i class="bi bi-geo-alt"></i>
        <ul class="dropdown-menu" aria-labelledby="dropdownMenuLink">
          <li><a class="dropdown-item" href="#">منطقه 1</a></li>
          <li><a class="dropdown-item" href="#">منطقه 2</a></li>
          <li><a class="dropdown-item" href="#">منطقه 3</a></li>
        </ul>
      </li>
    </ul>
    <div class="report mt-5">
      <div class="report-header">
        <button class="close-btn">X</button>
        <h6>رسیدگی به گزارش ها</h6>
      </div>
      <p>هنوز 20% گزارش ها باقی مانده است</p>
      <div class="progress">
        <div class="progress-bar w-75" role="progressbar" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100"></div>
      </div>
      <div class="actions"> 
        <a href="#">رسیدگی</a>
        <a href="#" style="color: rgb(138, 131, 131);">رد کردن</a>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.headerSide {
  display: flex;
  flex-direction: row-reverse;
  align-items: center;
  border-bottom: 2px solid #f6f6f6;
  padding-bottom: 10px;
  margin: 15px;

  img {
    width: 37px;
    border-radius: 10px;
    margin-left: 10px;
  }
}

.sidebar {
  width: 250px;
  height: 100%;
  position: fixed;
  right: 0;
  border-left: 2px solid #f6f6f6;
  text-align: right;
  padding-bottom: 20px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin: 12px 15px;
  font-size: 16px;
}

i {
  margin-left: 10px;
}

.report {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 10px;
  margin: 15px;
  text-align: right;
  background-color: #f3f3f3;

  .report-header {
    display: flex;
    justify-content: space-between;
    align-items: center;

    h6 {
      font-size: 15px;
      margin: 0;
    }

    .close-btn {
      background: none;
      border: none;
      font-size: 16px;
      cursor: pointer;
      margin-left: 10px;
    }
  }

  p {
    font-size: 12px;
    margin: 5px 0;
  }

  .actions {
    text-align: left;
    margin-top: 10px;
    display: flex;
    

    a {
      margin: 0 0 0 4px;
      color: #007bff;
      text-decoration: none;
      font-size: 12px;
    }
  }
}

.progress {
  height: 8px;
  width: 100%;
  max-width: 180px;
  margin: 0 auto;
}
</style>
