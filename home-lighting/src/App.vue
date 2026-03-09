<template>
  <div class="app-wrapper">
    <nav class="main-nav">
      <div class="container d-flex justify-content-between align-items-center">
        <div class="logo-area">
          <img src="@/assets/images/resim-tam.png" alt="Logo" class="logo">
        </div>
        <div class="nav-links">
          <router-link to="/">KRYEFAQJA</router-link>
          <router-link to="/about">RRETH NESH</router-link>
        </div>
        <a href="https://wa.me/38348722922" class="cta-contact">KONTAKT</a>
      </div>
    </nav>

    <router-view />

    <footer class="main-footer">
      <div class="container text-center">
        <h2 class="gold-text">HOME LIGHTING</h2>
        <p>Prizren, Kosovë | +383 48 722 922</p>
        <div class="social-links">
          <span>Instagram</span> • <span>Facebook</span>
        </div>
        <p class="copyright">© 2026 Home Lighting. All Rights Reserved.</p>
      </div>
    </footer>
  </div>
</template>

<style>
:root { --gold: #d4af37; --dark: #0a0a0a; --glass: rgba(255, 255, 255, 0.05); }
body { margin: 0; background: var(--dark) !important; color: white !important; font-family: 'Inter', sans-serif; }

.main-nav { position: fixed; top: 0; width: 100%; z-index: 1000; padding: 20px 0; background: rgba(0,0,0,0.7); backdrop-filter: blur(10px); border-bottom: 1px solid rgba(255,255,255,0.1); }
.logo { height: 90px; width: 110px; }
.nav-links a { color: white; text-decoration: none; margin: 0 15px; font-weight: 500; letter-spacing: 1px; }
.nav-links a.router-link-active { color: var(--gold); }
.cta-contact { background: var(--gold); color: black; text-decoration: none; padding: 8px 20px; border-radius: 50px; font-weight: 700; }

.main-footer { padding: 80px 0 40px; border-top: 1px solid #1a1a1a; margin-top: 100px; }
.gold-text { color: var(--gold); letter-spacing: 3px; }
.copyright { font-size: 0.8rem; color: #555; margin-top: 30px; }


.main-nav { 
  padding: 10px 0; 
}

@media (max-width: 768px) {
  .logo { height: 30px; }
  .nav-links { display: none; } 
  .cta-contact { font-size: 0.8rem; padding: 6px 15px; }
}
</style>