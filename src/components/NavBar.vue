<template>
  <nav>
    <router-link to="/" class="nav-items">View Projects</router-link>
    <router-link to="/add" class="nav-items">Add Project</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
* {
  margin: 0;
  color: white;
}
nav {
  height: 80px;
  background: rgb(51, 51, 51);
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.nav-items {
  text-decoration: none;
  list-style: none;
  color: white;
  font-family: "Roboto", sans-serif;
}
</style>
