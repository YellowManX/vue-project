<template>
  <div id="app">
    <h1>Quiz App</h1>
    <OperatorQuiz
      v-if="operator"
      @onBack="clearOperator"
      :operator="operator"
    />
    <OperatorSelector v-if="!operator" @changeOperator="changeOperator" />
  </div>
</template>

<script>
import { RouterLink, RouterView } from "vue-router";
import OperatorSelector from "@/components/OperatorSelector.vue";
import OperatorQuiz from "@/components/OperatorQuiz.vue";
export default {
  name: "app",
  data() {
    return {
      operator: null,
    };
  },
  methods: {
    changeOperator(operator) {
      this.operator = operator;
    },
    clearOperator() {
      this.operator = null;
    },
  },
  components: { OperatorSelector, OperatorQuiz },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
}
h1 {
  display: block;
  margin-bottom: 50px;
}
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 20px;
  color: #2c3e50;
}
button {
  padding: 10px;
  min-width: 80px;
  background-color: #10aeb2;
  color: white;
  border: none;
  font-size: 16px;
  cursor: pointer;
  border-radius: 50%;
}
</style>
