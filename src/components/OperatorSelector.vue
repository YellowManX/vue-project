<template>
  <div>
    <h3>Choose your favorite:</h3>
  </div>
  <div class="buttons">
    <button @click="$emit('changeOperator', '+')">Addition (+)</button>
    <button @click="$emit('changeOperator', '-')">Subtraction (-)</button>
    <button @click="$emit('changeOperator', '/')">Division(/)</button>
    <button @click="$emit('changeOperator', '*')">Multiplication(*)</button>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
h3 {
  margin-bottom: 15px;
}
.buttons {
  display: flex;
  gap: 15px;
}
</style>
