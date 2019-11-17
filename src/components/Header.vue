<template>
    <header class="header">
      <img src="../assets/attribution-logo.svg" alt="The Movie Database logo" class="header-logo">
      <router-link class="header-link" :to="{ name: 'Home' }">Search</router-link>
    </header>
</template>

<script>
export default {
    name: "Header"
}
</script>

<style>

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2rem 4rem;
  background-color: #2d3748;
  color: #fff;
  box-shadow:  0 4px 10px rgba(0, 0, 0, .2);
}

.header-logo {
  width: 4rem;
}

.header-link {
  color: #fff;
  justify-self: flex-end;
  text-decoration: none;
  font-size: 1.1rem;
  padding: .8rem 1.5rem;
}

</style>