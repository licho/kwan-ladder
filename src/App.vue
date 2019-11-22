<template>
  <div id="app">
    <img alt="Vue logo" src="https://www.kwantec.com/images/logo-white.png" class="logo">
    <HelloWorld msg="Bienvenido a la escalera de ping pong Kwan!"/>
    <Ladder/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Ladder from './components/Ladder.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Ladder
  }
}
</script>

<style scoped lang="less">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  .logo {
    width: 200px;
    margin-left: 130px;
  }
}
</style>
