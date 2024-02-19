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
    console.log(FazerConta())
}
</script>
<template>
    <div class="row bg-light pt-2 pb-4">
        <div class="me-5 col-md">
            <label class="text-center d-block pt-2 pb-2 fs-5 " for="number1">Digite um Número</label>
            <input id="number1" type="number" class="p-3 text-center form-control" v-model="estado.valor1" @keyup="FazerConta()" />
        </div>
        <div class="me-5 col-md">
            <label class="text-center d-block pt-2 pb-2 fs-5 " for="number2">Digite um Número</label>
            <input id="number2" type="number" class="p-3 text-center form-control" v-model="estado.valor2" @keyup="FazerConta()" />
        </div>
        <div class="col-md-3">
            <label class="text-center d-block pt-2 pb-2 fs-5 " for="select-option">Escolha a Operação</label>
            <select class="p-3 btn btn-primary w-100" @change="alterarFiltro($event)" id="select-option">
                <option value="somar">Somar</option>
                <option value="subtrair">Subtrair</option>
                <option value="multiplicar">Multiplicar</option>
                <option value="dividir">Dividir</option>
            </select>
        </div>
    </div>
    <div class="row bg-success-subtle mt-5">
        <h2 class="text-center pt-2 pb-2" v-if="FazerConta() != Infinity">
            O resultado da operação é <br /><b>{{ FazerConta().toFixed(2) }}</b>
        </h2>
    </div>
</template>


<style></style>