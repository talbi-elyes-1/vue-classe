<script setup lang="ts">
import { ref } from 'vue'

const ds = ref(0)
const tp = ref(0)
const ex = ref(0)

const moyenne = ref<number | null>(null)
const mention = ref('')

function calculerMoyenne() {
  moyenne.value = (ds.value + tp.value + ex.value) / 3

  if (moyenne.value >= 16) {
    mention.value = 'Très Bien'
  } else if (moyenne.value >= 14) {
    mention.value = 'Bien'
  } else if (moyenne.value >= 12) {
    mention.value = 'Assez Bien'
  } else if (moyenne.value >= 10) {
    mention.value = 'Passable'
  } else {
    mention.value = 'Insuffisant'
  }
}
</script>

<template>
  <div class="page">
    <div class="card">
      <h1>Calcul de Moyenne</h1>
      <p>Entrez les notes de la matière</p>

      <div class="form">
        <label>DS</label>
        <input v-model.number="ds" type="number" min="0" max="20">

        <label>TP</label>
        <input v-model.number="tp" type="number" min="0" max="20">

        <label>EX</label>
        <input v-model.number="ex" type="number" min="0" max="20">
      </div>

      <button @click="calculerMoyenne">
        Calculer
      </button>

      <div v-if="moyenne !== null" class="result">
        <h2>Moyenne : {{ moyenne.toFixed(2) }}/20</h2>
        <p>Mention : <strong>{{ mention }}</strong></p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.page {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, #667eea, #764ba2);
  font-family: Arial, sans-serif;
}

.card {
  background: white;
  padding: 35px;
  border-radius: 20px;
  width: 350px;
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

h1 {
  color: #333;
}

.card > p {
  color: #777;
}

.form {
  display: flex;
  flex-direction: column;
  text-align: left;
  margin: 25px 0;
}

label {
  margin-top: 10px;
  margin-bottom: 5px;
  font-weight: bold;
}

input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 16px;
}

button {
  padding: 12px 25px;
  border: none;
  border-radius: 8px;
  background: #667eea;
  color: white;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background: #5568d9;
}

.result {
  margin-top: 25px;
  padding: 15px;
  background: #f2f4ff;
  border-radius: 10px;
}

.result h2 {
  color: #333;
}

.result strong {
  color: #667eea;
}
</style>