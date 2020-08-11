<template>
  <div class="hello">
    <div class="1parte">
      <img class="logo" alt="Vue logo" src="../assets/logo.png" />
      <h1>{{ title }}</h1>
      <Error v-if="Error" />
      <form>
        <input
          class="input"
          type="text"
          v-model="tarea"
          placeholder="Ingrese nueva Tarea"
        />
        <input class="input" type="number" v-model="hora" />
        <button class="button" @click.prevent="addTarea">
          Añadir
        </button>
      </form>
    </div>

    <div class="parte2">
      <p v-if="tareas.length === 0" class="notiene">No tiene tareas 😉</p>
      <Tareas
        v-else
        :tareas="tareas"
        @eliminar="Eliminar"
        :totalHoras="totalHoras"
        @cambiar="cambiar"
      />
    </div>
  </div>
</template>

<script>
import Tareas from './Tareas'
import Error from './Error'
export default {
  components: { Tareas, Error },
  name: 'Formulario',
  data() {
    return {
      estado: false,
      Error: false,
      tarea: '',
      hora: 0,
      tareas: [],
      totalHoras: 0
    }
  },

  methods: {
    addTarea() {
      if (this.tarea === '' || this.hora === 0 || this.hora === '') {
        this.Error = true
        setTimeout(() => {
          this.Error = false
        }, 1000)
        return
      }
      this.totalHoras += parseInt(this.hora)
      this.tareas.push({
        tarea: this.tarea,
        hora: this.hora,
        estado: this.estado,
        totalHoras: this.totalHoras
      })

      this.tarea = ''
      this.hora = 0
      localStorage.setItem('tarea-vue', JSON.stringify(this.tareas))
    },
    Eliminar(index) {
      this.totalHoras -= this.tareas[index].hora
      this.tareas.splice(index, 1)
      localStorage.setItem('tarea-vue', JSON.stringify(this.tareas))
    },
    cambiar(index) {
      this.tareas[index].estado = true
      localStorage.setItem('tarea-vue', JSON.stringify(this.tareas))
    }
  },
  created() {
    let datosDB = JSON.parse(localStorage.getItem('tarea-vue'))
    if (datosDB === null) {
      this.tareas = []
    } else {
      this.tareas = datosDB
    }
  },
  props: {
    title: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../assets/sass/main.scss';
.logo {
  display: flex;
  justify-content: center;
  margin: 0 auto;
}
.hello {
  position: relative;
  & h1 {
    text-align: center;
  }
}

.input {
  font-family: $fuente2;
  width: 100%;
  display: block;
  margin-top: 10px;
  outline: none;
  padding: 10px;
  overflow: hidden;
  border-radius: 3px;
  border: 1px solid #5555;
  &:hover {
    box-shadow: 0.5px 0.5px 2px rgba(0, 0, 0, 0.5);
  }
}

.button {
  margin-top: 10px;
  background-color: $color-verse2;
  cursor: pointer;
  border-radius: 5px;
  text-decoration: none;
  padding: 7px;
  font-size: 1em;
  transition: 0.3s ease;
  display: inline-block;
  outline: none;
  color: $color-white;
  border: 0.1px $color-verse2 solid;
  box-shadow: 0.5px 0.5px 0.5px rgba(0, 0, 0, 0.6);
  &:hover {
    padding: 9px;
  }
}
.notiene {
  text-transform: uppercase;
  font-weight: 500;
  text-align: center;
}
</style>
