<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.jpg" class="logo">
    <div class="row">
      <div class="col">
          <FormularioVue :UsuariosRegistrados="UsuariosRegistrados" :RegistroTerminado="RegistroTerminado"></FormularioVue>
      </div>
      <div class="col">
          <TablaRegistro :UsuariosRegistrados="UsuariosRegistrados"></TablaRegistro>
      </div>
    </div>
  </div>
</template>

<script>
import FormularioVue from './components/FormularioVue.vue'
import TablaRegistro from './components/TablaRegistros.vue'

export default {
  name: 'App',
  components: {
    FormularioVue,
    TablaRegistro
  },
  data() {
    const UsuariosRegistrados = []
    return {
      UsuariosRegistrados
    }
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
  margin: 15pt;
}
.logo {
  width: 6em;
}
</style>
