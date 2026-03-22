<template>
  <main class="product-detail-container">
    <div class="container section">
      <button class="btn-back" @click="$router.push('/')">← Quay lại Menu</button>
      
      <div v-if="product" class="row g-5 align-items-center detail-row">
        <!-- Left Column: Image -->
        <div class="col-12 col-md-6 text-center">
          <div class="detail-img-box">
            <img :src="product.Image" :alt="product.Name" class="detail-img" />
          </div>
        </div>
        
        <!-- Right Column: Info -->
        <div class="col-12 col-md-6 detail-info">
          <span class="category-badge">{{ product.Category }}</span>
          <h1 class="detail-title">{{ product.Name }}</h1>
          <p class="detail-price">{{ formattedPrice }}</p>
          
          <div class="detail-desc-box">
            <h5>Thành phần / Mô tả</h5>
            <p class="detail-desc">{{ product.Description }}</p>
          </div>
          
          <div class="action-box">
            <!-- Quantity control -->
            <div class="quantity-control">
              <button class="btn-qty" @click="decreaseQty">-</button>
              <span class="qty-text">{{ quantity }}</span>
              <button class="btn-qty" @click="increaseQty">+</button>
            </div>
            
            <!-- Add to cart -->
            <button class="btn-add-large">Thêm vào giỏ hàng</button>
          </div>
        </div>
      </div>
      
      <!-- Fallback when product not found -->
      <div v-else class="text-center py-5 mt-5">
        <h2>Không tìm thấy sản phẩm!</h2>
        <p>Sản phẩm này không tồn tại hoặc đã bị xóa.</p>
        <button class="btn-add-large mt-4" style="flex: none; display: inline-block; width: auto;" @click="$router.push('/')">Về trang chủ</button>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import coffeeData from '../data/mockdata.json'

const route = useRoute()
const product = ref(null)
const quantity = ref(1)

onMounted(() => {
  const id = parseInt(route.params.id)
  product.value = coffeeData.find(item => item.ID === id)
})

const formattedPrice = computed(() => {
  if (!product.value || product.value.Price === undefined) return '0 ₫'
  return new Intl.NumberFormat('vi-VN', { 
    style: 'currency', 
    currency: 'VND' 
  }).format(product.value.Price)
})

const increaseQty = () => {
  quantity.value++
}

const decreaseQty = () => {
  if (quantity.value > 1) {
    quantity.value--
  }
}
</script>

<style scoped>
.product-detail-container {
  min-height: 80vh;
  padding: 40px 0;
  background-color: #f5ede0;
}
.btn-back {
  background: transparent;
  border: none;
  color: #7A6A5E;
  font-weight: 600;
  font-size: 15px;
  cursor: pointer;
  margin-bottom: 30px;
  display: inline-flex;
  align-items: center;
  transition: color 0.2s;
  padding: 0;
}
.btn-back:hover {
  color: #2c1a0e;
}
.detail-row {
  background: #fff;
  border-radius: 24px;
  padding: 40px;
  box-shadow: 0 10px 40px rgba(0,0,0,0.04);
}
.detail-img-box {
  background: #f7f0e6;
  border-radius: 16px;
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 400px;
}
.detail-img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  border-radius: 8px;
}
.category-badge {
  display: inline-block;
  background: #ede0ce;
  color: #7a6a5e;
  padding: 6px 14px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 16px;
}
.detail-title {
  font-size: 42px;
  font-weight: 800;
  color: #2c1a0e;
  margin-bottom: 10px;
  line-height: 1.2;
}
.detail-price {
  font-size: 28px;
  font-weight: 800;
  color: #c9a882;
  margin-bottom: 30px;
}
.detail-desc-box {
  margin-bottom: 40px;
  border-top: 1px solid #eee;
  padding-top: 20px;
}
.detail-desc-box h5 {
  font-size: 16px;
  font-weight: 700;
  color: #2c1a0e;
  margin-bottom: 10px;
}
.detail-desc {
  font-size: 15px;
  color: #666;
  line-height: 1.6;
}
.action-box {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-top: 20px;
}
.quantity-control {
  display: flex;
  align-items: center;
  background: #f5ede0;
  border-radius: 30px;
  padding: 4px 6px;
}
.btn-qty {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: none;
  background: #fff;
  color: #2c1a0e;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 2px 5px rgba(0,0,0,0.05);
  transition: all 0.2s;
}
.btn-qty:hover {
  background: #ede0ce;
}
.qty-text {
  width: 40px;
  text-align: center;
  font-size: 18px;
  font-weight: 700;
  color: #2c1a0e;
}
.btn-add-large {
  flex: 1;
  background: #2c6fad;
  color: #fff;
  border: none;
  border-radius: 30px;
  padding: 16px 24px;
  font-size: 16px;
  font-weight: 700;
  cursor: pointer;
  box-shadow: 0 8px 20px rgba(44, 111, 173, 0.3);
  transition: all 0.3s;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
.btn-add-large:hover {
  background: #1b5490;
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(44, 111, 173, 0.4);
}

@media (max-width: 768px) {
  .detail-row {
    padding: 20px;
  }
  .detail-title {
    font-size: 32px;
  }
  .action-box {
    flex-direction: column;
    align-items: stretch;
  }
  .quantity-control {
    justify-content: center;
    padding: 8px;
  }
}
</style>
