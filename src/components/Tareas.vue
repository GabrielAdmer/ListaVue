<template>
  <div>
    <div
      class="tarea"
      v-for="(item, index) in tareas"
      :key="index"
      :class="{ fondo: tareas[index].estado }"
    >
      <div class="tarea_izquieda">
        <button class="button-ok" @click="cambiar(index)">&OK</button>
        <p>{{ item.tarea }}</p>
        <p>{{ item.hora }} horas</p>
      </div>
      <button class="button" @click="Delete(index)">&&times</button>
    </div>
    <div class="total_horas">
      <p>Leva {{ totalHoras }} horas Estudiando</p>
    </div>
  </div>
</template>

<script>
export default {
  // props: { tareas: Array, totalHoras: Number },
  props: { tareas: Array, totalHoras: Number },

  methods: {
    Delete(index) {
      this.$emit('eliminar', index)
    },
    cambiar(index) {
      this.$emit('cambiar', index)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/sass/main.scss';
.fondo {
  background-color: $color-verder;
}
.tarea {
  margin-top: 10px;
  border-radius: 5px;
  border: 1px solid #3333;
  display: flex;
  justify-content: space-between;
  align-items: center;
  & p {
    margin: 0;
    padding: 0 10px;
  }
  &_izquieda {
    display: flex;
  }
}
.button {
  background-color: $color-rojo;
  cursor: pointer;
  border-radius: 5px;
  text-decoration: none;
  padding: 7px;
  font-size: 1em;
  transition: 0.3s ease;
  display: inline-block;
  outline: none;
  color: $color-white;
  border: 0.1px $color-rojo solid;
  box-shadow: 0.5px 0.5px 0.5px rgba(0, 0, 0, 0.6);
  &:hover {
    padding: 9px;
  }
}
.button-ok {
  background-color: $color-amarillo;
  cursor: pointer;
  border-radius: 5px;
  text-decoration: none;
  padding: 7px;
  font-size: 1em;
  transition: 0.3s ease;
  display: inline-block;
  outline: none;
  color: $color-white;
  border: 0.1px $color-amarillo solid;
  box-shadow: 0.5px 0.5px 0.5px rgba(0, 0, 0, 0.6);
  &:hover {
    padding: 9px;
  }
}
</style>
