<script setup lang="ts">
import { ref } from 'vue'

const compteur = ref(0)
const scoreSauvegarde = ref<number | null>(null)

function augmenter() {
  compteur.value++
}

function diminuer() {
  compteur.value--
}

function reinitialiser() {
  compteur.value = 0
}

function sauvegarderScore() {
  scoreSauvegarde.value = compteur.value
}
</script>

<template>
  <div class="page">
    <div class="card">
      <div class="icon">🔢</div>

      <h1>Mon Compteur</h1>
      <p class="description">Un compteur réalisé avec Vue.js</p>

      <div class="counter">
        <button class="btn minus" @click="diminuer">
          −
        </button>

        <div class="number">
          {{ compteur }}
        </div>

        <button class="btn plus" @click="augmenter">
          +
        </button>
      </div>

      <div class="actions">
        <button class="reset" @click="reinitialiser">
          🔄 Réinitialiser
        </button>

        <button class="save" @click="sauvegarderScore">
          💾 Sauvegarder mon score
        </button>
      </div>

      <p class="message">
        Valeur actuelle : <strong>{{ compteur }}</strong>
      </p>

      <p v-if="scoreSauvegarde !== null" class="saved">
        ⭐ Score sauvegardé : <strong>{{ scoreSauvegarde }}</strong>
      </p>
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
  padding: 45px;
  border-radius: 25px;
  text-align: center;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.25);
  min-width: 350px;
}

.icon {
  font-size: 45px;
  margin-bottom: 10px;
}

h1 {
  margin: 0;
  color: #333;
  font-size: 32px;
}

.description {
  color: #777;
  margin-bottom: 35px;
}

.counter {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 25px;
}

.number {
  min-width: 80px;
  font-size: 55px;
  font-weight: bold;
  color: #333;
}

.btn {
  width: 60px;
  height: 60px;
  border: none;
  border-radius: 50%;
  font-size: 32px;
  color: white;
  cursor: pointer;
  transition: 0.2s;
}

.minus {
  background: #e74c3c;
}

.plus {
  background: #2ecc71;
}

.btn:hover {
  transform: scale(1.12);
}

.actions {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 30px;
}

.reset,
.save {
  padding: 12px 20px;
  border: none;
  border-radius: 10px;
  color: white;
  font-size: 15px;
  cursor: pointer;
  transition: 0.2s;
}

.reset {
  background: #f39c12;
}

.save {
  background: #3498db;
}

.reset:hover,
.save:hover {
  transform: scale(1.03);
}

.message {
  margin-top: 30px;
  color: #666;
}

.message strong {
  color: #667eea;
}

.saved {
  color: #27ae60;
  margin-top: 15px;
}
</style>