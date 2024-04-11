<script setup>
import { reactive } from 'vue';

const estado = reactive({
    N1: '',
    N2: '',
    operacaoSelecionada: '',
    operacoes: {
        soma: (a, b) => a + b,
        subtracao: (a, b) => a - b,
        multiplicacao: (a, b) => a * b,
        divisao: (a, b) => (b !== 0 ? a / b : 'Não existe divisão por 0'),
    },
    resultado: 0,
});

const calcularOperacao = () => {
    const num1 = parseFloat(estado.N1);
    const num2 = parseFloat(estado.N2);

    if (!isNaN(num1) && !isNaN(num2)) {
        estado.resultado = estado.operacoes[estado.operacaoSelecionada](num1, num2);
    }
}

const limparResultado = () => {
    estado.resultado = '';
}
</script>


<template>
    <form @submit.prevent="calcularOperacao">
        <div class="row">
            <h1 class="row-text text-center">Calculadora VueJS</h1>
            <div class="col">
                <input type="number" v-model="estado.N1" class="form-control text-center" @blur="limparResultado"
                    required>
                <input type="number" v-model="estado.N2" class="form-control text-center mt-1" @blur="limparResultado"
                    required>
                <div class="col">
                    <select v-model="estado.operacaoSelecionada" class="form-control mt-3 text-center"
                        @change="calcularOperacao">
                        <option value="" disabled>Escolha a operação:</option>
                        <option value="soma">Soma</option>
                        <option value="subtracao">Subtração</option>
                        <option value="divisao">Divisão</option>
                        <option value="multiplicacao">Multiplicação</option>
                    </select>
                </div>
                <p class="mt-3 text-center fs-2 fw-bold">Resultado: {{ estado.resultado }}</p>
            </div>
        </div>
    </form>
</template>

<style scoped>
.row {
    background-color: rgb(226, 226, 226);
    padding: 1em;
    border-radius: 10px;

    h1 {
        color: green;
    }
}
</style>
