<template>
    <div>
      <center>
        <h1 style="font-family: 'Courier New', Courier, monospace;">MAT239 Project II, Yona Voss-Andreae</h1>
        <div class="maindiv">
          <Sim1 ref="sim1" />
          <Sim2 />
          <Sim3 />
        </div>
      </center>
    </div>
</template>

<script>

import Sim1 from './components/Sim1.vue'
import Sim2 from './components/Sim2.vue'
import Sim3 from './components/Sim3.vue'

export default {
  name: 'App',
  components: {
    Sim1,
    Sim2,
    Sim3
  },
  mounted() {
    this.$refs.sim1.rolldice()
  }
}
</script>

<style>
.maindiv {
    border: black solid 3px;
    /* border-radius: 1%; */
    background-color: lightblue;
    display: inline-flex;
    /* padding-bottom: 10%; */
    font-family: 'Courier New', Courier, monospace;
    margin: 2px;
}
</style>
