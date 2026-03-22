<template>
  <main class="home-container">
    <!-- ===================== HERO ===================== -->
    <section class="hero">
      <img
        src="https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?w=1400&q=90"
        alt="Coffee Banner"
        class="hero-bg-img"
      />
      <div class="hero-overlay"></div>
      <div class="hero-content">
        <div class="hero-row">
          <span class="hero-text-left">ORDER</span>
          <span class="hero-text-right">COFFEE</span>
        </div>
        <div class="hero-row">
          <span class="hero-welcome">Welcome</span>
        </div>
      </div>
    </section>

    <!-- ===================== FEATURED SPECIALS ===================== -->
    <section class="section featured-section">
      <h2 class="section-title">Featured Specials</h2>
      <div class="row g-4">
        <div v-for="item in featuredItems" :key="item.ID" class="col-6 col-md-3">
          <ProductCard :product="item" />
        </div>
      </div>
    </section>

    <!-- ===================== MENU ===================== -->
    <section class="section menu-section">
      <div class="menu-header">
        <div>
          <h2 class="menu-title">Menu</h2>
          <span class="menu-subtitle">drinks</span>
        </div>
        <button class="btn-basket">my basket</button>
      </div>

      <div class="categories">
        <button
          v-for="cat in categories"
          :key="cat.label"
          :class="['cat-pill', { active: cat.label === activeCategory }]"
          @click="activeCategory = cat.label"
        >
          {{ cat.label }}
        </button>
      </div>

      <div class="row g-3">
        <div
          v-for="item in filteredMenu"
          :key="item.ID"
          class="col-6 col-md-3"
        >
          <ProductCard :product="item" />
        </div>
      </div>
    </section>
  </main>
</template>

<script setup>
import { ref, computed } from 'vue'
import ProductCard from '../components/ProductCard.vue'
import coffeeData from '../data/mockdata.json'

// Nổi bật: 4 món đầu tiên từ Mockdata
const featuredItems = coffeeData.slice(0, 4)

const categories = [
  { label: 'Iced coffee', tag: 'iced' },
  { label: 'Milk-Based Coffee', tag: 'milk' },
  { label: 'Classic Coffee', tag: 'classic' },
  { label: 'Specialty Coffee', tag: 'specialty' },
  { label: 'Sweet Coffee', tag: 'sweet' }
]

const activeCategory = ref('Iced coffee')

// Toàn bộ menu từ Mockdata.Json
const allMenu = coffeeData

const tagMap = {
  'Iced coffee': 'iced',
  'Milk-Based Coffee': 'milk',
  'Classic Coffee': 'classic',
  'Specialty Coffee': 'specialty',
  'Sweet Coffee': 'sweet'
}

const filteredMenu = computed(() => {
  const tag = tagMap[activeCategory.value]
  return tag ? allMenu.filter(i => i.Category === tag) : allMenu
})
</script>

<style scoped>
/* ===== HERO ===== */
.hero {
  position: relative;
  width: 100%;
  height: 400px;
  overflow: hidden;
}
.hero-bg-img {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center 40%;
  z-index: 0;
}
.hero-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.25);
  z-index: 1;
}
.hero-content {
  position: absolute;
  inset: 0;
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 0 5%;
}
.hero-row {
  display: flex;
  align-items: baseline;
  gap: 220px;
}
.hero-row:last-child {
  gap: 0;
  justify-content: flex-end;
  width: 100%;
  padding-right: 6%;
  margin-top: -12px;
}
.hero-text-left,
.hero-text-right {
  font-size: 88px;
  font-weight: 900;
  color: #fff;
  letter-spacing: 6px;
  text-transform: uppercase;
  text-shadow: 0 2px 24px rgba(0,0,0,0.30);
  line-height: 1;
}
.hero-welcome {
  font-family: 'Georgia', serif;
  font-style: italic;
  font-size: 42px;
  color: #fff;
  font-weight: 400;
  text-shadow: 0 2px 16px rgba(0,0,0,0.25);
}

/* ===== SECTIONS ===== */
.section {
  max-width: 1100px;
  margin: 0 auto;
  padding: 50px 5%;
}
.section-title {
  font-size: 26px;
  font-weight: 800;
  margin: 0 0 28px 0;
  color: #2c1a0e;
}

/* ===== MENU ===== */
.menu-section { padding-top: 10px; }
.menu-header { display: flex; justify-content: space-between; align-items: flex-end; margin-bottom: 0; }
.menu-title { font-size: 32px; font-weight: 900; color: #2c1a0e; margin: 0; }
.menu-subtitle { font-family: 'Georgia', cursive; font-style: italic; font-size: 18px; color: #2c6fad; display: block; margin-top: -4px; }
.btn-basket {
  background: #c9a882;
  color: #fff;
  border: none;
  padding: 10px 28px;
  border-radius: 24px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
}
.btn-basket:hover { background: #b08d74; }

.categories { display: flex; gap: 10px; margin: 22px 0; flex-wrap: wrap; }
.cat-pill {
  padding: 8px 20px;
  border-radius: 24px;
  border: none;
  background: #d4c4b0;
  color: #fff;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s;
}
.cat-pill.active { background: #2c6fad; }
.cat-pill:hover { background: #2c6fad; }

/* ===== RESPONSIVE ===== */
@media (max-width: 960px) {
  .hero-text-left, .hero-word { font-size: 60px; }
}
@media (max-width: 640px) {
  .hero { flex-direction: column; justify-content: center; }
  .hero-text-left, .hero-text-right { font-size: 40px; }
}
</style>
