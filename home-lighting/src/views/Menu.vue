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
              <div class="d-flex justify-content-between align-items-center mt-3">
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
  { id: 1, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 2, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 3, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 4, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
  { id: 1, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 2, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 3, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 4, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
  { id: 1, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 2, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 3, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 4, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
  { id: 1, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 2, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 3, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 4, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
  { id: 1, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 2, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 3, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 4, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
  { id: 1, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 2, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 3, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 4, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
  { id: 1, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 2, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 3, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 4, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
  { id: 1, name: 'Llambadar Modern', brand: 'Cata', price: 125, cat: 'Brendshëm', img: hm3 },
  { id: 2, name: 'Ndriçues Muri', brand: 'Ave', price: 45, cat: 'Jashtëm', img: hm5 },
  { id: 3, name: 'Spotlight Pro', brand: 'FSL', price: 85, cat: 'Brendshëm', img: hm3 },
  { id: 4, name: 'Elegance Gold', brand: 'Crown', price: 65, cat: 'Brendshëm', img: hm5 },
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
  top: 0; 
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}
.bg-img { 
  width: 100%;
  height: 100%; 
  object-fit: cover;
  filter: blur(15px) brightness(0.4);
  transform: scale(1.1);
  transition: 0.8s;
}
.light-ambiance { 
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle, transparent 20%, rgba(0,0,0,0.9) 100%);
  transition: 0.8s;
}

.light-on .light-ambiance {
  background: radial-gradient(circle, rgba(255, 244, 214, 0.15) 0%, rgba(212, 175, 55, 0.1) 100%), rgba(255, 253, 245, 0.7);
}
.light-on .bg-img { 
  filter: blur(12px) brightness(0.8); 
}
.light-on .main-title, .light-on .product-title {
  color: #1a1a1a !important; 
}
.light-on .glass-card { 
  background: rgba(255, 255, 255, 0.4); 
  border-color: rgba(0,0,0,0.05); 
}
.dark-mode .main-title, .dark-mode .product-title {
  color: #ffffff !important; 
}

.category-pills {
  display: flex;
  justify-content: center;
  gap: 15px; flex-wrap: wrap; 
}
.btn-cat {
  border: none; padding: 10px 25px; 
  border-radius: 50px;
  font-weight: 600;
  font-size: 0.9rem;
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  cursor: pointer;
  background: rgba(255, 255, 255, 0.1);
  color: #fff;
  backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}
.btn-cat:hover {
   transform: translateY(-3px) scale(1.05);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3); 
}
.btn-cat.all.active {
   background: #6c757d; 
   box-shadow: 0 0 20px rgba(108, 117, 125, 0.4); 
}
.btn-cat.indoor.active { 
  background: #d4af37;
  color: #000;
  box-shadow: 0 0 20px rgba(212, 175, 55, 0.5);
}
.btn-cat.outdoor.active {
   background: #2ecc71; 
   color: #000;
  box-shadow: 0 0 20px rgba(46, 204, 113, 0.5); 
}
.light-on .btn-cat:not(.active) {
  background: rgba(0, 0, 0, 0.05);
  color: #333;
  border-color: rgba(0, 0, 0, 0.1); 
}

.glass-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  overflow: hidden; 
  transition: 0.5s;
}

.text-gold { 
  color: #d4af37 !important;
  font-weight: 800;
}

.img-container {
   height: 200px; 
   overflow: hidden;
}

.img-container img {
  width: 100%;
  height: 100%;
  object-fit: cover; 
  transition: 0.5s;
}

.glass-card:hover .img-container img {
   transform: scale(1.1);
}

.price-tag {
  color: #d4af37;
  font-weight: 700;
  font-size: 1.2rem;
}

.btn-add-plus {
  background: #d4af37;
  border: none; width: 35px;
  height: 35px; border-radius: 10px;
  color: #000; font-weight: 900;
  transition: 0.3s; 
}

.controls-wrapper {
  position: fixed;
  top: 20px;
  right: 20px;
  z-index: 1000;
  display: flex;
  gap: 10px; 
}

.btn-control {
  background: rgba(255,255,255,0.15);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255,255,255,0.2);
  width: 50px; 
  height: 50px;
  border-radius: 50%;
  color: #fff;
  font-size: 1.2rem;
  cursor: pointer; 
  transition: 0.3s;
}

.light-on .btn-control {
  color: #000; 
  border-color: rgba(0,0,0,0.1);
  background: rgba(0,0,0,0.05); 
}

.cart-drawer {
  position: fixed;
  top: 0;
  right: -350px;
  width: 320px;
  height: 100%;
  background: rgba(0,0,0,0.85);
  backdrop-filter: blur(20px);
  z-index: 2000;
  transition: 0.4s; 
  padding: 25px; 
  color: #fff; 
}

.cart-drawer.open { 
  right: 0;
}

.mini-item {
  display: flex;
  align-items: center;
  gap: 10px; 
  margin-bottom: 15px;
  border-bottom: 1px solid rgba(255,255,255,0.1);
  padding-bottom: 10px; 
}

.mini-item img { 
  width: 45px;
  height: 45px;
  border-radius: 8px;
  object-fit: cover; 
}

.btn-wa-order { 
  width: 100%; 
  background: #25d366;
  color: white;
  border: none;
  padding: 12px;
  border-radius: 12px;
  font-weight: bold;
  margin-top: 20px;
}

@media (max-width: 768px) { 
  .img-container 
  { height: 160px;
  }
   .cart-drawer 
   { width: 100%;
     right: -100%;
  } 
   .btn-cat { padding: 8px 18px;
     font-size: 0.8rem; 
  }
}

</style>