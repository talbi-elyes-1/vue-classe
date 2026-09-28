<script setup lang="ts">
import { ref, computed } from 'vue'

const nouvelleTache = ref('')

const taches = ref([
  { id: 1, texte: 'Réviser Vue', terminee: false },
  { id: 2, texte: 'Préparer le TP', terminee: false }
])

const tachesRestantes = computed(() => {
  return taches.value.filter(tache => !tache.terminee).length
})

function ajouterTache() {
  if (nouvelleTache.value.trim() === '') {
    return
  }

  taches.value.push({
    id: Date.now(),
    texte: nouvelleTache.value,
    terminee: false
  })

  nouvelleTache.value = ''
}

function supprimerTache(id: number) {
  taches.value = taches.value.filter(tache => tache.id !== id)
}
</script>

<template>
  <div class="page">
    <div class="card">
      <h1>📝 Ma liste de tâches</h1>

      <form @submit.prevent="ajouterTache" class="form">
        <input
          v-model="nouvelleTache"
          type="text"
          placeholder="Ajouter une tâche..."
        />

        <button type="submit">
          Ajouter
        </button>
      </form>

      <p class="counter">
        {{ tachesRestantes }} tâche(s) restante(s)
      </p>

      <div v-if="taches.length === 0" class="empty">
        Aucune tâche pour le moment.
      </div>

      <ul v-else class="task-list">
        <li
          v-for="tache in taches"
          :key="tache.id"
          :class="{ terminee: tache.terminee }"
        >
          <label>
            <input
              v-model="tache.terminee"
              type="checkbox"
            />

            <span>{{ tache.texte }}</span>
          </label>

          <button
            class="delete"
            @click="supprimerTache(tache.id)"
          >
            Supprimer
          </button>
        </li>
      </ul>
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
  width: 500px;
  padding: 35px;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

h1 {
  text-align: center;
  color: #333;
}

.form {
  display: flex;
  gap: 10px;
  margin: 25px 0;
}

.form input {
  flex: 1;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 8px;
  color: #333;
  background: white;
}

.form input::placeholder {
  color: #888;
}

.form button {
  padding: 12px 20px;
  border: none;
  border-radius: 8px;
  background: #667eea;
  color: white;
  cursor: pointer;
}

.counter {
  text-align: center;
  color: #667eea;
  font-weight: bold;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px;
  margin-top: 10px;
  background: #f4f5ff;
  border-radius: 8px;
  color: #333;
}

.task-list li label {
  display: flex;
  gap: 10px;
  align-items: center;
  color: #333;
}

.task-list li span {
  color: #333;
}

.terminee span {
  text-decoration: line-through;
  color: #888;
}

.delete {
  border: none;
  background: #e74c3c;
  color: white;
  padding: 7px 12px;
  border-radius: 6px;
  cursor: pointer;
}

.form button:hover,
.delete:hover {
  opacity: 0.85;
}

.empty {
  text-align: center;
  color: #888;
  margin-top: 25px;
}
</style>