<template>
  <div class="about-page">
    <section class="about-hero">
      <div class="container text-center">
        <h1 class="display-4 fw-bold">Rreth Nesh</h1>
        <p class="lead">Lider në ndriçimin modern në Kosovë që nga viti 2010.</p>
      </div>
    </section>

    <section class="container my-5 py-5">
      <div class="row align-items-center">
        <div class="col-md-6">
          <h2 class="mb-4" style="color: #78d5ef;">Historia Jonë</h2>
          <p>
            Home Lighting ka filluar si një dyqan i vogël me një vizion të madh: 
            të sjellë dritën dhe stilin në çdo shtëpi. Sot, ne ofrojmë koleksionet 
            më ekskluzive të ndriçimit të brendshëm, të jashtëm dhe industrial.
          </p>
          <ul class="list-unstyled mt-4">
            <li>✅ <strong>Kualitet:</strong> Produkte nga markat më të njohura evropiane.</li>
            <li>✅ <strong>Inovacion:</strong> Teknologjia më e fundit LED dhe Smart.</li>
            <li>✅ <strong>Përvojë:</strong> Mbi 15 vite eksperiencë në projektim.</li>
          </ul>
        </div>
        <div class="col-md-6">
          <div class="img-frame">
            <img src="@/assets/images/home-lighting-jasht.png" alt="Home Lighting Store" class="img-fluid rounded-4 shadow-lg">
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.about-page {
  background: #0f1113;
  color: #fff;
  min-height: 100vh;
  padding-top: 80px;
}

.about-hero {
  background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), url('@/assets/images/home-lighting-jasht.png');
  background-size: cover;
  background-position: center;
  padding: 100px 0;
  border-bottom: 2px solid #78d5ef;
}

.img-frame {
  border: 1px solid rgba(120, 213, 239, 0.3);
  padding: 15px;
  border-radius: 25px;
  background: rgba(255,255,255,0.02);
}

h2 {
  font-weight: 700;
}

p {
  line-height: 1.8;
  color: #ccc;
}
</style>