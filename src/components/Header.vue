<template>
  <div class="dashboard mt-2">
    <div class="main-content">
      <header class="header">
        <div class="user-info">
          <img src="https://www.pngall.com/wp-content/uploads/5/Woman-Face-PNG-Download-Image.png" alt="User" class="avatar" />
          <i class="bi bi-bell"></i>
          <i class="bi bi-search"></i>
        </div>
        <div class="header-details">
          <h3>نقشه</h3>
          <h6>موقعیت مکانی اسکوترها و سایر موارد</h6>
        </div>
      </header>
    </div>
    <Sidebar />
  </div>
</template>

<style lang="scss" scoped>
$primary-font-size: 20px;
$header-height: 50px;
$border-color: #f6f6f6;
$avatar-size: 40px;

.dashboard {
  display: flex;
}

.main-content {
  flex: 1;
  padding-right: 220px;
}

.header {
  height: $header-height;
  background-color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 20px;
  border-bottom: 2px solid $border-color;
}

.user-info {
  display: flex;
  align-items: center;
}

.avatar {
  width: $avatar-size;
  height: $avatar-size;
  border-radius: 50%;
}

.bi-search, .bi-bell {
  margin-left: $primary-font-size;
  color: #000;
  font-size: $primary-font-size;
}

.header-details {
  text-align: right;
}
</style>
