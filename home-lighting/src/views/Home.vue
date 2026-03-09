<template>
  <div class="home-page">
    <section class="hero-full">
      <div class="hero-overlay">
        <div class="container text-center" v-motion-fade>
          <h4 class="text-gold letter-spacing">ART & DESIGN</h4>
          <h1 class="hero-title fw-bold mb-4">DRITA QË JEP <br> JETË AMBIENTIT</h1>
          <p class="hero-text mb-5 opacity-75">Zbuloni koleksionet më të fundit të ndriçimit modern në Prizren.</p>
          <router-link to="/menu" class="btn-explore">EKSPLORO KOLEKSIONIN</router-link>
        </div>
      </div>
    </section>

    <section class="brands-bar py-4 py-md-5">
      <div class="container d-flex justify-content-around align-items-center flex-wrap gap-3 opacity-50 grayscale">
        <img src="@/assets/images/cata.png" alt="Cata" class="brand-img">
        <img src="@/assets/images/ave.png" alt="Ave" class="brand-img">
        <img src="@/assets/images/fsl.png" alt="FSL" class="brand-img">
        <img src="@/assets/images/crown.png" alt="Crown" class="brand-img">
      </div>
    </section>

    <section id="products" class="container py-4 py-md-5">
      <div class="section-title mb-4 mb-md-5">
        <h2 class="display-5 fw-bold">PRODUKTET <span class="text-gold">ELITE.</span></h2>
        <div class="line"></div>
      </div>

      <div class="row g-2 g-md-4">
        <div v-for="p in products" :key="p.id" class="col-6 col-md-6 col-lg-4">
          <div class="product-card">
            <div class="product-img">
              <img :src="p.img" :alt="p.name" class="img-fluid">
              <div class="product-overlay">
                <button @click="order(p.name)" class="btn-wa">POROSIT</button>
              </div>
            </div>
            <div class="product-info p-2 p-md-4">
              <span class="p-brand d-none d-md-block">{{ p.brand }}</span>
              <h3 class="p-name h6 h5-md">{{ p.name }}</h3>
              <div class="d-flex justify-content-between align-items-center mt-2 mt-md-3">
                <span class="p-price text-gold fw-bold mb-0">{{ p.price }}€</span>
                <span class="p-status d-none d-sm-inline">Në Stok</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import hm3 from '@/assets/images/hm3.png'
import hm5 from '@/assets/images/hm5.png'

const products = ref([
  { id: 1, name: 'Llambadar Modern Crystal', brand: 'Cata', price: 125, img: hm3 },
  { id: 2, name: 'Ndriçues Muri LED Silver', brand: 'Ave', price: 45, img: hm5 },
  { id: 3, name: 'Reflektor Pro Outdoor', brand: 'FSL', price: 89, img: hm3 },
  { id: 4, name: 'Dritë Elegance Gold', brand: 'Crown', price: 65, img: hm5 },
  { id: 5, name: 'Led Panel Slim', brand: 'Cata', price: 15, img: hm3 },
  { id: 6, name: 'Spotlight Industrial', brand: 'Ave', price: 75, img: hm5 },
])

const order = (name) => window.open(`https://wa.me/38348722922?text=Përshëndetje, interesohem për ${name}`, '_blank')
</script>

<style scoped>
.hero-full {
  height: 90vh;
  background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), url('@/assets/images/home-lighting-jasht.png');
  background-size: cover;
  background-position: center; 
  display: flex;
  align-items: center;
}

.hero-title {
  font-size: calc(1.8rem + 3vw);
}

.text-gold { 
  color: #d4af37 !important;
}

.letter-spacing {
  letter-spacing: 3px;
}

.btn-explore { 
  border: 1px solid white;
  color: white;
  padding: 12px 30px;
  text-decoration: none; 
  letter-spacing: 2px;
  transition: 0.3s;
  font-size: 0.9rem;
}

.btn-explore:hover { 
  background: white;
  color: black;
}

.brand-img {
  height: 25px;
  filter: brightness(0) invert(1);
}

.grayscale { 
  filter: grayscale(1); 
}

.product-card {
  background: #111;
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid #222;
  transition: 0.4s;
  height: 100%;
}

.product-card:hover { 
  transform: translateY(-10px);
  border-color: #d4af37;
}

.product-img { position: relative;
  overflow: hidden;
  height: 250px;
} 

@media (min-width: 768px) { .product-img { height: 350px; } }

.product-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: 0.5s;
}

.product-overlay { 
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0; 
  transition: 0.3s; 
}

.btn-wa { 
  background: #d4af37;
  border: none;
  padding: 8px 15px;
  font-weight: 700; 
  color: black; 
  font-size: 0.8rem;
  border-radius: 5px;
}


@media (max-width: 768px) {
  .product-overlay { opacity: 1; background: transparent; align-items: flex-end; padding-bottom: 10px; }
  .btn-wa { font-size: 0.7rem; padding: 5px 10px; box-shadow: 0 4px 15px rgba(0,0,0,0.5); }
  .hero-full { height: 60vh; }
  .hero-text { font-size: 0.9rem; }
}

.product-card:hover .product-overlay {
   opacity: 1;
}

.p-brand {
  font-size: 0.6rem; 
  color: #555;
  text-transform:
  uppercase;
  letter-spacing: 2px;
}

.p-name { 
  margin: 5px 0;
  font-size: 0.9rem;
}

@media (min-width: 768px) { .p-name { font-size: 1.25rem; } }

.p-price {
  font-size: 1rem;
}

@media (min-width: 768px) { .p-price { font-size: 1.5rem; } }

.p-status {
  font-size: 0.6rem;
  color: #2ecc71;
  background: rgba(46, 204, 113, 0.1);
  padding: 2px 8px;
  border-radius: 10px;
}

.line { 
  width: 40px;
  height: 2px;
  background: #d4af37;
}

</style>