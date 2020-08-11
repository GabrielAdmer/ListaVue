<template>
  <div class="error">
    <p>Datos obligatoros</p>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
@import '../assets/sass/main.scss';
.error p {
  width: 100%;
  top: 0;
  border: 1px solid $color-rojo;
  background-color: $color-rojo;
  color: $color-white;
  text-align: center;
  padding: 5px;
  position: absolute;
}
</style>
