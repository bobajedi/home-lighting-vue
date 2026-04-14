<template>
  <div class="menu-page" :class="isLightOn ? 'light-on' : 'dark-mode'">
    
    <div class="background-overlay">
      <img src="@/assets/images/home-lighting-jasht.png" alt="BG" class="bg-img">
      <div class="light-ambiance"></div>
    </div>
    
    <div class="controls-wrapper">
      <button class="btn-control" @click="isLightOn = !isLightOn" :title="isLightOn ? 'Fikni Dritat' : 'Ndizni Dritat'">
        {{ isLightOn ? '🌑' : '💡' }}
      </button>
      <button class="btn-control cart-btn" @click="showCart = !showCart">
        🛒 <span v-if="cart.length" class="badge">{{ cart.length }}</span>
      </button>
    </div>

    <div class="cart-drawer" :class="{ 'open': showCart }">
      <div class="cart-header">
        <h4>Shporta Juaj</h4>
        <button @click="showCart = false" class="close-btn">✕</button>
      </div>
      <div class="cart-items">
        <div v-for="(item, i) in cart" :key="i" class="mini-item">
          <img :src="item.img" alt="">
          <div class="mini-details">
            <h6>{{ item.name }}</h6>
            <p>{{ item.price }}€</p>
          </div>
          <button @click="removeFromCart(i)" class="remove-item">✕</button>
        </div>
      </div>
      <div class="cart-footer" v-if="cart.length">
        <button @click="sendWhatsApp" class="btn-wa-order">Dërgo në WhatsApp</button>
      </div>
    </div>

    <div class="container content-area py-5">
      <header class="text-center mb-5 mt-4">
        <h1 class="display-4 fw-bold main-title">KATALOGU <span class="text-gold">ELITE</span></h1>
        
        <div class="category-pills mt-4">
          <button 
            @click="activeCat = 'Të gjitha'" 
            :class="['btn-cat all', { active: activeCat === 'Të gjitha' }]">
            Të gjitha
          </button>
          <button 
            @click="activeCat = 'Brendshëm'" 
            :class="['btn-cat indoor', { active: activeCat === 'Brendshëm' }]">
            Brendshëm
          </button>
          <button 
            @click="activeCat = 'Jashtëm'" 
            :class="['btn-cat outdoor', { active: activeCat === 'Jashtëm' }]">
            Jashtëm
          </button>
        </div>
      </header>

      <div class="row g-3 g-md-4">
        <div v-for="p in filteredProducts" :key="p.id" class="col-6 col-md-4 col-lg-3">
          <div class="glass-card">
            <div class="img-container">
              <img :src="p.img" :alt="p.name">
            </div>
            <div class="p-3 card-content">
              <h3 class="product-title">{{ p.name }}</h3>
              <div class="d-flex justify-content-between align-items-center mt-auto">
                <span class="price-tag">{{ p.price }}€</span>
                <button @click="addToCart(p)" class="btn-add-plus">+</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import hm3 from '@/assets/images/hm3.png'
import hm5 from '@/assets/images/hm5.png'

const isLightOn = ref(false) 
const showCart = ref(false)
const cart = ref([])
const activeCat = ref('Të gjitha')

const products = ref([
  { id: 1, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 2, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 3, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 4, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
  { id: 5, name: 'Llambadar Modern 2', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 6, name: 'Ndriçues Muri 2', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 7, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 8, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 9, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 10, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
  { id: 11, name: 'Llambadar Modern 2', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 12, name: 'Ndriçues Muri 2', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 13, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 14, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 15, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 16, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
  { id: 17, name: 'Llambadar Modern 2', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 18, name: 'Ndriçues Muri 2', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
])

const filteredProducts = computed(() => {
  return activeCat.value === 'Të gjitha' ? products.value : products.value.filter(p => p.cat === activeCat.value)
})

const addToCart = (p) => { cart.value.push(p); showCart.value = true; }
const removeFromCart = (i) => cart.value.splice(i, 1)

const sendWhatsApp = () => {
  let msg = "Përshëndetje! Dua të porosis:\n"
  cart.value.forEach(item => msg += `- ${item.name} (${item.price}€)\n`)
  window.open(`https://wa.me/38348722922?text=${encodeURIComponent(msg)}`, '_blank')
}
</script>

<style scoped>
.menu-page {
  min-height: 100vh;
  position: relative;
  overflow-x: hidden;
  transition: all 0.8s ease;
}
.background-overlay { 
  position: fixed; 
  top: 0; left: 0;
  width: 100%; height: 100%;
  z-index: -1;
}
.bg-img { 
  width: 100%; height: 100%; 
  object-fit: cover;
  filter: blur(15px) brightness(0.4);
  transform: scale(1.1);
  transition: 0.8s;
}
.light-ambiance { 
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: radial-gradient(circle, transparent 20%, rgba(0,0,0,0.9) 100%);
  transition: 0.8s;
}


.light-on .light-ambiance {
  background: radial-gradient(circle, rgba(255, 244, 214, 0.15) 0%, rgba(212, 175, 55, 0.1) 100%), rgba(255, 253, 245, 0.7);
}
.light-on .bg-img { filter: blur(12px) brightness(0.8); }
.light-on .main-title, .light-on .product-title { color: #1a1a1a !important; }
.light-on .glass-card { background: rgba(255, 255, 255, 0.5); border-color: rgba(0,0,0,0.05); }


.dark-mode .main-title, .dark-mode .product-title { color: #ffffff !important; }


.category-pills {
  display: flex;
  justify-content: center;
  gap: 12px; flex-wrap: wrap; 
}
.btn-cat {
  border: none; padding: 10px 22px; 
  border-radius: 50px;
  font-weight: 600;
  font-size: 0.85rem;
  transition: 0.3s;
  cursor: pointer;
  background: rgba(255, 255, 255, 0.1);
  color: #fff;
  backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}
.btn-cat.active { transform: scale(1.05); }
.btn-cat.all.active { background: #6c757d; }
.btn-cat.indoor.active { background: #d4af37; color: #000; }
.btn-cat.outdoor.active { background: #2ecc71; color: #000; }

.glass-card {
  height: 100%; 
  display: flex;
  flex-direction: column;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  overflow: hidden; 
  transition: 0.4s ease;
}

.card-content {
  flex-grow: 1; 
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.img-container {
   height: 180px; 
   overflow: hidden;
   background: rgba(255,255,255,0.03);
}

.img-container img {
  width: 100%;
  height: 100%;
  object-fit: cover; 
  transition: 0.5s;
}

.product-title {
  font-size: 0.95rem;
  font-weight: 600;
  margin-bottom: 10px;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  min-height: 2.8em; 
}

.price-tag {
  color: #d4af37;
  font-weight: 700;
  font-size: 1.1rem;
}

.btn-add-plus {
  background: #d4af37;
  border: none; width: 32px; height: 32px;
  border-radius: 8px;
  color: #000; font-weight: 800;
  transition: 0.2s;
}

.controls-wrapper {
  position: fixed;
  top: 15px; right: 15px;
  z-index: 1000;
  display: flex; gap: 10px; 
}

.btn-control {
  background: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255,255,255,0.1);
  width: 45px; height: 45px;
  border-radius: 50%;
  color: #fff;
  cursor: pointer; 
}

.cart-drawer {
  position: fixed;
  top: 0; right: -100%;
  width: 300px; height: 100%;
  background: rgba(15, 15, 15, 0.95);
  backdrop-filter: blur(20px);
  z-index: 2000;
  transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  padding: 20px; color: #fff; 
}
.cart-drawer.open { right: 0; }
@media (max-width: 768px) { 
  .img-container { height: 140px; }
  .product-title { font-size: 0.85rem; min-height: 2.6em; }
  .price-tag { font-size: 1rem; }
  .cart-drawer { width: 85%; }
  .main-title { font-size: 1.8rem; }
  
  .btn-cat { padding: 8px 15px; font-size: 0.75rem; }
  
  .row.g-3 {
    --bs-gutter-x: 0.6rem;
    --bs-gutter-y: 0.6rem;
  }
  
  .controls-wrapper {
    top: auto;
    bottom: 20px; 
  }
}
</style>