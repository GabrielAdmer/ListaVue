<template>
  <div id="app">
    <Formulario title="Lista de tareas" />
  </div>
</template>

<script>
import Formulario from './components/Formulario.vue'

export default {
  name: 'App',
  components: {
    Formulario
  }
}
</script>

<style lang="scss">
@import './assets/sass/main.scss';

#app {
  font-family: $fuente1;
  margin: 10px;
}
</style>
