<template>
  <LogoImg></LogoImg>
  <FiltersBar></FiltersBar>
</template>

<script>
import FiltersBar from './components/FiltersBar.vue'
import LogoImg from './components/LogoImg.vue'

export default {
  name: 'App',
  components: {
    LogoImg,
    FiltersBar
  }
}
</script>

<style lang="scss">
body {
  background-color: #e9e2de;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
