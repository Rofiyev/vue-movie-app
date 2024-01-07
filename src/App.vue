<template>
  <section>
    <HeaderComponent />
    <main>
      <router-view />
    </main>
  </section>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'

export default {
  components: { HeaderComponent }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Aladin&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Aladin', handwriting;
}
*::selection {
  background: rgba(66, 184, 131, 0.5);
}
body {
  background: #35495e;
}
</style>
