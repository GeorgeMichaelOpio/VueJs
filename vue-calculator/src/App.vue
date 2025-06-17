<template>
  <div id="app">
    <h1>Vue.js Calculator</h1>
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/AppCalculator.vue'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
  background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

#app {
  max-width: 500px;
  width: 100%;
  text-align: center;
  color: white;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

h1 {
  margin-bottom: 30px;
  font-size: 2.5rem;
  font-weight: 600;
  letter-spacing: 1px;
}
</style>