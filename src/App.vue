<template>
  <div id="app">
    <h1>Explore the Cosmos</h1>
    <p class='description'>Click either button to see daily photos of our solar system.</p>
    <HelloWorld/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
body {
  background-color: #19042A;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

h1 {
  color: #FFFFFF;
  font-size: 60px;
  font-family: 'Coiny';
  text-shadow: -1px 0 #71298F, 0 1px #71298F, 1px 0 #71298F, 0 -1px #71298F;

}

.description {
  font-size: 30px;
  color: #71298F;
  font-family: 'Raleway', sans-serif;
  text-shadow: -1px 0 #3A078D, 0 1px #3A078D, 1px 0 #3A078D, 0 -1px #3A078D;

}

</style>
