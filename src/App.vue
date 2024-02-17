<script setup lang="ts">
import { reactive } from "vue";

interface State {
  // Defina o formato dos dados aqui
  // Por exemplo:
  valor1: number;
  valor2: number;
  filtro: string;
}
const estado = reactive<State>({
  valor1: 0,
  valor2: 0,
  filtro: "somar",
});

function FazerConta(): number {
  const { filtro, valor1, valor2 } = estado;

  switch (filtro) {
    case "subtrair":
      return valor1 - valor2;
    case "multiplicar":
      return valor1 * valor2;
    case "dividir":
      return valor1 / valor2;
    default:
      return valor1 + valor2;
  }
}
function alterarFiltro(e: Event) {
  const target = e.target as HTMLInputElement;
  estado.filtro = target.value;
  FazerConta();
}
</script>

<template>
  <div class="container">
    <h1 class="text-center p-5">Calculadora Aritmética</h1>
    <div class="row">
      <input
        type="number"
        class="col-md p-3 text-center me-5"
        v-model="estado.valor1"
        @keyup="FazerConta()"
      />
      <input
        type="number"
        class="col-md p-3 text-center me-5"
        v-model="estado.valor2"
        @keyup="FazerConta()"
      />
      <select class="col-md-2 p-3" @change="alterarFiltro($event)">
        <option value="somar">Somar</option>
        <option value="subtrair">Subtrair</option>
        <option value="multiplicar">Multiplicar</option>
        <option value="dividir">Dividir</option>
      </select>
    </div>
    <div class="row">
      <h2 class="text-center mt-5" v-if="FazerConta() != 0">
        O resultado da operação é <br /><b>{{ FazerConta().toFixed(2) }}</b>
      </h2>
    </div>
  </div>
</template>

<style scoped>
</style>
