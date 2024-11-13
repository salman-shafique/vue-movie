<template>
  <nav class="main-header navbar navbar-expand-md">
    <div class="container-fluid d-flex justify-content-between align-items-center">
      <!-- Mobile View: Hamburger Icon -->
      <button
          class="navbar-toggler d-md-none me-2"
          type="button"
          @click="isCollapsed = !isCollapsed"
          aria-controls="navbarMain"
          aria-expanded="false"
          aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <!-- Logo Text in Center -->
      <span class="navbar-brand logo-text">TMDB</span>

      <!-- Right Side Icons on Mobile -->
      <div class="d-flex align-items-center d-md-none">
        <a class="nav-link p-2" href="#"><i class="bi bi-search"></i></a>
        <a class="nav-link p-2" href="#"><i class="bi bi-person"></i></a>
      </div>

      <!-- Collapsible Navbar Content -->
      <div v-show="isCollapsed" class="navbar-collapse" id="navbarMain">
        <ul class="navbar-nav me-auto">
          <li class="nav-item"><a class="nav-link" href="#">Movies</a></li>
          <li class="nav-item"><a class="nav-link" href="#">TV Shows</a></li>
          <li class="nav-item"><a class="nav-link" href="#">People</a></li>
        </ul>

        <!-- Desktop View: EN, Login, Join TMDB -->
        <div class="navbar-nav ms-auto d-none d-md-flex">
          <button class="btn btn-outline-light btn-sm me-2">EN</button>
          <a class="nav-link login-link" href="#">Login</a>
          <a class="nav-link join-link" href="#">Join TMDB</a>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const isCollapsed = ref(false);
    return { isCollapsed };
  },
};
</script>

<style scoped>
.main-header {
  background-color: #0d253f;
  color: white;
  padding: 10px 20px;
}

.logo-text {
  color: white;
  font-weight: bold;
  font-size: 1.2rem;
}

.navbar-toggler {
  border: none;
}

.navbar-toggler-icon {
  filter: brightness(0) invert(1);
}

.navbar-nav .nav-link {
  color: white !important; /* Ensure the nav links are white */
}

.nav-link i {
  color: white;
  font-size: 1.2rem;
}

.btn-outline-light {
  color: #01b4e4;
  background-color: white;
  font-weight: bold;
}

.login-link, .join-link {
  color: white;
  margin-left: 10px;
}

.join-link {
  font-weight: bold;
}
</style>
