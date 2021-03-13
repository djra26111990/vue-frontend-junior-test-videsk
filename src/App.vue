<template>
  <div id="app" class="bg-gray-100">
    <NavBar />
    <Breadcrumbs />
    <Home />
  </div>
</template>

<script>
import Home from './Views/Home'
import NavBar from './Components/NavBar'
import Breadcrumbs from './Components/Breadcrumbs'

export default {
  name: 'app',
  components: { Home, NavBar, Breadcrumbs }
}
</script>

<style lang="postcss">
@tailwind base;
@tailwind components;
@tailwind utilities;

html, body, #app {
  width: 100%;
  height: 100%;
  margin: 0;
  overflow: auto;
  box-sizing: border-box;
}

@media (min-width: 768px) {
  .chart-container {
  position: relative;
  height: 70vh;
  width: 25vw;
  padding: 10px
}
}

@media (max-width: 767px) {
  .chart-container {
  position: relative;
  height: 70vh;
  width: auto;
  padding: 10px
}
}

</style>
