<script setup lang="ts">
import { ref, computed } from 'vue'

const poids = ref('')
const taille = ref('')

const moyenne = computed(() => {
  const kg = Number(poids.value)
  const metres = Number(taille.value) / 100

  if (kg <= 0 || metres <= 0) {
    return null
  }

  return kg / (metres * metres)
})

const categorie = computed(() => {
  if (moyenne.value === null) {
    return ''
  }

  if (moyenne.value < 18.5) {
    return 'Insuffisance pondérale'
  } else if (moyenne.value < 25) {
    return 'Corpulence normale'
  } else if (moyenne.value < 30) {
    return 'Surpoids'
  } else {
    return 'Obésité'
  }
})

function effacer() {
  poids.value = ''
  taille.value = ''
}
</script>

<template>
  <div class="page">
    <div class="card">
      <div class="icon">⚖️</div>

      <h1>Calculateur d'IMC</h1>
      <p class="description">
        Entrez votre poids et votre taille
      </p>

      <div class="form">
        <label>
          Poids (kg)
          <input
            v-model="poids"
            type="number"
            min="1"
            placeholder="Ex : 70"
          />
        </label>

        <label>
          Taille (cm)
          <input
            v-model="taille"
            type="number"
            min="50"
            placeholder="Ex : 175"
          />
        </label>
      </div>

      <button class="reset" @click="effacer">
        🔄 Effacer
      </button>

      <div v-if="moyenne !== null" class="result">
        <h2>Votre IMC</h2>

        <div class="number">
          {{ moyenne.toFixed(1) }}
        </div>

        <p>
          Catégorie :
          <strong>{{ categorie }}</strong>
        </p>
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
  padding: 40px;
  border-radius: 20px;
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  width: 350px;
}

.icon {
  font-size: 40px;
}

h1 {
  color: #333;
}

.description {
  color: #777;
}

.form {
  text-align: left;
  margin: 25px 0;
}

label {
  display: block;
  margin-bottom: 15px;
  font-weight: bold;
}

input {
  width: 100%;
  box-sizing: border-box;
  padding: 10px;
  margin-top: 6px;
  border: 1px solid #ccc;
  border-radius: 8px;
}

.reset {
  padding: 10px 25px;
  border: none;
  border-radius: 8px;
  background: #667eea;
  color: white;
  cursor: pointer;
}

.result {
  margin-top: 25px;
  padding: 20px;
  background: #f2f4ff;
  border-radius: 10px;
}

.number {
  font-size: 45px;
  font-weight: bold;
  color: #667eea;
}

.result strong {
  color: #667eea;
}
</style>