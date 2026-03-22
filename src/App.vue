<template>
  <div class="drinko-app">

    <!-- ===================== NAVBAR ===================== -->
    <nav class="navbar-custom">
      <div class="navbar-inner">
        <div class="brand">Drinko</div>
        <div class="nav-links">
          <a href="#" class="active">Home</a>
          <a href="#">Menu</a>
          <a href="#">Delivery</a>
        </div>
        <div class="nav-icons">
          <span class="icon">♡</span>
          <span class="icon">👤</span>
          <span class="icon">🛒</span>
        </div>
      </div>
    </nav>

    <!-- NỘI DUNG TRANG (ĐƯỢC QUẢN LÝ BỞI VUE ROUTER) -->
    <RouterView />

    <!-- ===================== FOOTER ===================== -->
    <footer class="site-footer">
      <div class="footer-inner">
        <div class="footer-col">
          <h5>☕ Drinko Coffee</h5>
          <p>Hương vị cà phê nguyên bản, rang xay mỗi ngày. Cam kết mang đến trải nghiệm tuyệt vời nhất.</p>
        </div>
        <div class="footer-col">
          <h5>Sản phẩm</h5>
          <ul>
            <li><a href="#">Cà phê pha máy</a></li>
            <li><a href="#">Cold Brew</a></li>
            <li><a href="#">Cà phê phin</a></li>
            <li><a href="#">Dụng cụ pha chế</a></li>
          </ul>
        </div>
        <div class="footer-col">
          <h5>Hỗ trợ</h5>
          <ul>
            <li><a href="#">Chính sách giao hàng</a></li>
            <li><a href="#">Đổi trả sản phẩm</a></li>
            <li><a href="#">Hướng dẫn mua hàng</a></li>
            <li><a href="#">Câu hỏi thường gặp</a></li>
          </ul>
        </div>
        <div class="footer-col">
          <h5>Liên hệ</h5>
          <p>📍 123 Đường Cà Phê, Quận 1, TP. HCM</p>
          <p>✉️ hi@drinko.vn</p>
          <p>📞 +84 123 456 789</p>
        </div>
      </div>
      <div class="footer-bottom">
        <p>© 2026 Drinko Coffee. All rights reserved.</p>
      </div>
    </footer>

  </div>
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<style scoped>
/* ===== GLOBAL ===== */
.drinko-app {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f5ede0;
  color: #2c1a0e;
  min-height: 100vh;
}

/* ===== NAVBAR ===== */
.navbar-custom {
  background-color: #fff;
  padding: 0 5%;
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 1px 8px rgba(0,0,0,0.06);
}
.navbar-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 60px;
  max-width: 1200px;
  margin: 0 auto;
}
.brand {
  font-size: 20px;
  font-weight: 800;
  color: #2c1a0e;
  letter-spacing: 1px;
}
.nav-links {
  display: flex;
  gap: 32px;
}
.nav-links a {
  text-decoration: none;
  font-size: 14px;
  color: #888;
  font-weight: 500;
  transition: color 0.2s;
}
.nav-links a.active, .nav-links a:hover {
  color: #2c1a0e;
}
.nav-icons {
  display: flex;
  gap: 18px;
  font-size: 18px;
  cursor: pointer;
}

/* Hủy bớt các class không liên quan tới layout ở App.vue */

/* ===== FOOTER ===== */
.site-footer {
  background-color: #2c1a0e;
  color: #e8d5b0;
  padding: 50px 0 0 0;
  margin-top: 20px;
}
.footer-inner {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1.5fr;
  gap: 40px;
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 5% 40px;
}
.footer-col h5 {
  color: #c9a882;
  font-size: 16px;
  font-weight: 700;
  margin-bottom: 16px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
.footer-col p {
  font-size: 14px;
  line-height: 1.7;
  color: #bba990;
  margin: 0 0 6px;
}
.footer-col ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
.footer-col ul li { margin-bottom: 8px; }
.footer-col ul li a {
  color: #bba990;
  text-decoration: none;
  font-size: 14px;
  transition: color 0.2s;
}
.footer-col ul li a:hover { color: #c9a882; }
.footer-bottom {
  background-color: #1a0e07;
  text-align: center;
  padding: 16px;
  font-size: 13px;
  color: #7a6a5e;
}
.footer-bottom p { margin: 0; }

@media (max-width: 768px) {
  .footer-inner {
    grid-template-columns: 1fr 1fr;
  }
}
@media (max-width: 480px) {
  .footer-inner {
    grid-template-columns: 1fr;
  }
}
</style>