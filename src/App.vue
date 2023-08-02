<template>
  <main>
    <div class="links">
      <RouterLink active-class="active" to="/">Home</RouterLink>
      <RouterLink active-class="active" to="/about">About</RouterLink>
    </div>
    <RouterView />
  </main>
</template>

<script>
import { RouterView, RouterLink } from "vue-router";
</script>

<style scoped>
.links {
  padding: 20px;
}

.links a {
  margin: 0 5px;
}

.active {
  font-weight: bold;
  color: orangered;
}
</style>