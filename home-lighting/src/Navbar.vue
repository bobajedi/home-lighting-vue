<template>
  <nav class="navbar navbar-expand-lg navbar-dark custom-navbar" id="ftco-navbar">
    <div class="container">
      <router-link to="/" class="logo-link">
        <img src="@/assets/images/resim-tam.png" alt="Home Lighting Logo" width="100" height="auto" class="logo">
      </router-link>

      <div class="icon">
        <span class="icon-phone"></span> +383 48 722 922 <br> +383 48 733 433
      </div>

      <div class="titulli-1">
        <span class="h-span">Home</span><br>
        <span class="l-span">Lighting</span>
      </div>

      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#ftco-nav">
        <span class="oi oi-menu"></span> Menu
      </button>

      <div class="collapse navbar-collapse" id="ftco-nav">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item">
            <router-link to="/" class="nav-link" active-class="active">Kryefaqja</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/about" class="nav-link" active-class="active">Rreth Nesh</router-link>
          </li>
          <li class="nav-item">
            <a href="https://api.whatsapp.com/send/?phone=38348722922" target="_blank" class="nav-link">Kontakt</a>
          </li>
          <li class="nav-item">
            <a href="https://maps.google.com" target="_blank" class="nav-link">Lokacioni</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script setup>
</script>

<style scoped>
</style>