<script setup>
import { reactive, computed } from 'vue';

// Estado que armazena os valores dos inputs e a operação selecionada
const estado = reactive({
  primeiroNumero: 0,
  segundoNumero: 0,
  operacao: 'soma', // Operação padrão
});

// Função computada que realiza o cálculo automaticamente sempre que um valor muda
const resultado = computed(() => {
  const { primeiroNumero, segundoNumero, operacao } = estado;
  const num1 = parseFloat(primeiroNumero);
  const num2 = parseFloat(segundoNumero);

  // Se não for um número válido, retorna 0
  if (isNaN(num1) || isNaN(num2)) return 0;

  switch (operacao) {
    case 'soma':
      return num1 + num2;
    case 'subtracao':
      return num1 - num2;
    case 'multiplicacao':
      return num1 * num2;
    case 'divisao':
      return num2 !== 0 ? num1 / num2 : 'Erro (Divisão por zero)';
    default:
      return 0;
  }
});
</script>

<template>
  <div class="container">
    <header>
      <h1>Calculadora Aritmética</h1>
      <p>VueJS - Cálculo em tempo real</p>
    </header>

    <main class="calculadora">
      <div class="campo">
        <label>Primeiro Número:</label>
        <input 
          type="number" 
          v-model="estado.primeiroNumero" 
          placeholder="0"
        />
      </div>

      <div class="campo">
        <label>Operação:</label>
        <select v-model="estado.operacao">
          <option value="soma">Soma (+)</option>
          <option value="subtracao">Subtração (-)</option>
          <option value="multiplicacao">Multiplicação (×)</option>
          <option value="divisao">Divisão (÷)</option>
        </select>
      </div>

      <div class="campo">
        <label>Segundo Número:</label>
        <input 
          type="number" 
          v-model="estado.segundoNumero" 
          placeholder="0"
        />
      </div>

      <div class="resultado-box">
        <span>O resultado é:</span>
        <div class="valor">{{ resultado }}</div>
      </div>
    </main>
  </div>
</template>

<style scoped>
/* Estilização para deixar a interface limpa e organizada */
.container {
  max-width: 400px;
  margin: 60px auto;
  padding: 20px;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-align: center;
}

header h1 {
  margin-bottom: 5px;
  color: #2c3e50;
}

header p {
  color: #7f8c8d;
  font-size: 0.9em;
  margin-bottom: 30px;
}

.calculadora {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.campo {
  display: flex;
  flex-direction: column;
  text-align: left;
  gap: 5px;
}

label {
  font-weight: bold;
  font-size: 0.85em;
  color: #34495e;
}

input, select {
  padding: 12px;
  border: 1px solid #dcdde1;
  border-radius: 8px;
  font-size: 16px;
  outline: none;
  transition: border-color 0.3s;
}

input:focus, select:focus {
  border-color: #3498db;
}

.resultado-box {
  margin-top: 20px;
  padding: 20px;
  background-color: #f1f2f6;
  border-radius: 8px;
}

.resultado-box span {
  display: block;
  font-size: 0.9em;
  color: #7f8c8d;
  margin-bottom: 5px;
}

.valor {
  font-size: 28px;
  font-weight: bold;
  color: #2ecc71;
}
</style>