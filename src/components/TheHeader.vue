<template>
  <header>
    <nav>
      <router-link to="/" class="logo">
        <img src="../assets/ranek.svg" alt="store" />
      </router-link>
      <!-- <router-link class="btn" to="/login">Vender / Login </router-link> -->
    </nav>
  </header>
</template>

<script>
export default {
  name: "TheHeader",
};
</script>

<style #scoped>
nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 20px;
  background: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.logo {
  padding: 10px 0;
  display: block;
  width: 100px;
}
.logo img {
  max-width: 90px;
}
</style>
