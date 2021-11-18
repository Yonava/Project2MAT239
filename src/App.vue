<template>
    <div id="app">
        <Sim2 />
    </div>
</template>

<script>

// import Sim1 from './components/Sim1.vue'
import Sim2 from './components/Sim2.vue'
// import Sim3 from './components/Sim3.vue'

export default {
  name: 'App',
  components: {
    // Sim1,
    Sim2,
    // Sim3
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
