<template>
  <header>
    <RouterLink :to="{ name: 'home' }">
      <h1><span>Vue </span>Movies</h1>
    </RouterLink>
  </header>
</template>

<script>
export default {}
</script>

<style scoped>
a {
  text-decoration: none;
}
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 16px;
  background-color: #2c3d4e;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
}
h1 {
  color: white;
  font-size: 28px;
}
h1 span {
  color: #42b883;
}
</style>
