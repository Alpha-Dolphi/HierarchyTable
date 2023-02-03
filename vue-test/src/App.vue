<style>
:root {
  --box-shadow: #999999;
  --box-border: #c6c9cb;
  --input-outline: #8bcbd8b9;
  --prime-dark-color: rgb(77, 81, 82);
  --prime-light-color: rgb(255, 255, 255);
}

* {
  padding: 0;
  margin: 0;
  color: var(--prime-dark-color);
  box-sizing: border-box;
  font-family: sans-serif;
}

body {
  font-size: 1.2rem;
}
</style>

<template>
  <div id="app">
    <AppLayout tableData="tableData" />
  </div>
</template>

<script>
import AppLayout from './components/AppLayout.vue'

export default {
  name: 'App',
  components: {
    AppLayout
  }
}
</script>
