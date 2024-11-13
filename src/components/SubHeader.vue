<template>
  <div class="sub-header navbar navbar-expand-md justify-content-center">
    <div class="container-fluid justify-content-center">
      <ul class="navbar-nav mx-auto flex-row">
        <li class="nav-item">
          <a class="nav-link active" href="#">Overview</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Media</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Fandom</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Share</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.sub-header {
  background-color: #01b4e4;
  padding: 8px 0;
}

.navbar-nav .nav-link {
  color: white;
  font-weight: bold;
  margin: 0 10px;
}

.navbar-nav .nav-link.active {
  border-bottom: 2px solid white;
}
</style>
