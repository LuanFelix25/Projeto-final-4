<script setup>
import { ref, onMounted, computed } from 'vue'
import { useStore } from 'vuex'

// This view no longer performs external HTTP requests (axios) for this deliverable.
// Instead we initialize the store with sample data and provide a small form
// with validation logic implemented here in the <script> block (requirement).

const store = useStore()
const loading = ref(false)
const error = ref(null)

// simple sample todos to seed the app (no network)
const sampleTodos = [
  { id: 1, title: 'Aprender Vue 3' },
  { id: 2, title: 'Praticar Router e Vuex' },
  { id: 3, title: 'Refatorar para Vite' },
]

onMounted(() => {
  // seed the store only if empty
  if (!store.state.todos || store.state.todos.length === 0) {
    store.commit('setTodos', sampleTodos)
  }
})

// Form + validation (migrated to view script per requirements)
const form = ref({ title: '' })
const formErrors = ref({ title: null })

function validate() {
  formErrors.value.title = null
  if (!form.value.title || !form.value.title.trim()) {
    formErrors.value.title = 'O título é obrigatório.'
  } else if (form.value.title.trim().length < 3) {
    formErrors.value.title = 'O título deve ter ao menos 3 caracteres.'
  }
  return !formErrors.value.title
}

function submit() {
  if (!validate()) return
  const title = form.value.title.trim()
  store.commit('addTodo', { title })
  form.value.title = ''
}

const todos = computed(() => store.state.todos || [])
</script>

<template>
  <section>
    <h2>🏠 Home (Router)</h2>
    <p>Lista de tarefas (armazenadas no <code>Vuex</code>).</p>

    <form @submit.prevent="submit" style="margin:.75rem 0; display:flex; gap:.5rem; align-items:center;">
      <input v-model="form.title" placeholder="Nova tarefa" style="padding:.45rem .6rem;" />
      <button type="submit" style="padding:.4rem .8rem;">Adicionar</button>
      <div style="color:#c00; font-size:.9rem; margin-left:.5rem;">{{ formErrors.title }}</div>
    </form>

    <ul>
      <li v-for="t in todos" :key="t.id">
        <strong>#{{ t.id }}</strong> — {{ t.title }}
      </li>
    </ul>

    <p v-if="$store.state.lastFetch" style="font-size:.9rem;color:#666;">
      Última atualização local: {{ new Date($store.state.lastFetch).toLocaleString() }}
    </p>
  </section>
</template>
