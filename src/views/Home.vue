<script setup>
import { ref, onMounted, computed } from 'vue'
import { useStore } from 'vuex'

const store = useStore()
const loading = ref(false)
const error = ref(null)

const sampleTodos = [
  { id: 1, title: 'Aprender Vue 3' },
  { id: 2, title: 'Praticar Router e Vuex' },
  { id: 3, title: 'Refatorar para Vite' },
]

onMounted(() => {
  if (!store.state.todos || store.state.todos.length === 0) {
    store.commit('setTodos', sampleTodos)
  }
})

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
  <section class="home-section">
    <div class="card">
      <div class="card-header">
        <h2>🏠 Home (Router)</h2>
        <p class="subtitle">Lista de tarefas armazenadas no <span class="highlight">Vuex</span></p>
      </div>

      <form @submit.prevent="submit" class="todo-form">
        <div class="form-group">
          <input 
            v-model="form.title" 
            placeholder="Digite uma nova tarefa..." 
            class="input"
            :class="{ 'input-error': formErrors.title }"
          />
          <button type="submit" class="btn btn-primary">
            <span>➕</span> Adicionar
          </button>
        </div>
        <transition name="error-fade">
          <div v-if="formErrors.title" class="error-message">
            ⚠️ {{ formErrors.title }}
          </div>
        </transition>
      </form>

      <div class="todos-container">
        <transition-group name="list" tag="ul" class="todo-list">
          <li v-for="t in todos" :key="t.id" class="todo-item">
            <span class="todo-id">#{{ t.id }}</span>
            <span class="todo-title">{{ t.title }}</span>
            <span class="todo-check">✓</span>
          </li>
        </transition-group>
        
        <div v-if="todos.length === 0" class="empty-state">
          <p>📋 Nenhuma tarefa ainda. Adicione uma acima!</p>
        </div>
      </div>

      <div v-if="$store.state.lastFetch" class="last-update">
        🕐 Última atualização: {{ new Date($store.state.lastFetch).toLocaleString() }}
      </div>
    </div>
  </section>
</template>

<style scoped>
.home-section {
  display: flex;
  justify-content: center;
}

.card {
  background: white;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  padding: 2rem;
  width: 100%;
  max-width: 700px;
  animation: slideUp 0.5s ease;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.card-header {
  margin-bottom: 1.5rem;
}

.card-header h2 {
  font-size: 1.8rem;
  color: #333;
  margin-bottom: 0.5rem;
}

.subtitle {
  color: #666;
  font-size: 1rem;
}

.highlight {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 600;
}

.todo-form {
  margin-bottom: 2rem;
}

.form-group {
  display: flex;
  gap: 0.75rem;
  margin-bottom: 0.5rem;
}

.input {
  flex: 1;
  padding: 0.9rem 1.2rem;
  border: 2px solid #e0e0e0;
  border-radius: 10px;
  font-size: 1rem;
  transition: all 0.3s ease;
  outline: none;
}

.input:focus {
  border-color: #667eea;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
}

.input-error {
  border-color: #ff4444;
}

.btn {
  padding: 0.9rem 1.5rem;
  border: none;
  border-radius: 10px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.btn-primary {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 16px rgba(102, 126, 234, 0.3);
}

.btn-primary:active {
  transform: translateY(0);
}

.error-message {
  color: #ff4444;
  font-size: 0.9rem;
  padding: 0.5rem;
  background: #ffe0e0;
  border-radius: 6px;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.error-fade-enter-active,
.error-fade-leave-active {
  transition: all 0.3s ease;
}

.error-fade-enter-from,
.error-fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.todos-container {
  margin-top: 1.5rem;
}

.todo-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.todo-item {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  padding: 1rem 1.5rem;
  border-radius: 10px;
  display: flex;
  align-items: center;
  gap: 1rem;
  transition: all 0.3s ease;
  cursor: pointer;
}

.todo-item:hover {
  transform: translateX(5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.todo-id {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  font-weight: 700;
  padding: 0.3rem 0.7rem;
  border-radius: 6px;
  font-size: 0.85rem;
}

.todo-title {
  flex: 1;
  color: #333;
  font-weight: 500;
}

.todo-check {
  color: #4caf50;
  font-size: 1.3rem;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.todo-item:hover .todo-check {
  opacity: 1;
}

.empty-state {
  text-align: center;
  padding: 3rem 1rem;
  color: #999;
  font-size: 1.1rem;
}

.last-update {
  margin-top: 1.5rem;
  padding: 0.75rem;
  background: #f8f9fa;
  border-radius: 8px;
  color: #666;
  font-size: 0.9rem;
  text-align: center;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.4s ease;
}

.list-enter-from {
  opacity: 0;
  transform: translateX(-30px);
}

.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.list-move {
  transition: transform 0.4s ease;
}

@media (max-width: 768px) {
  .card {
    padding: 1.5rem;
  }
  
  .form-group {
    flex-direction: column;
  }
  
  .btn {
    width: 100%;
    justify-content: center;
  }
  
  .todo-item {
    padding: 0.85rem 1rem;
  }
}

  font-size: 0.95rem;
}

@media (min-width: 640px) {
  .hero-actions { flex-direction: column; }
}

@media (min-width: 900px) {
  .hero-actions { flex-direction: column; }
  .btn-hero { max-width: 520px; }
}

@media (max-width: 480px) {
  .hero-card { padding: 1.6rem; }
  .hero-card h1 { font-size: 1.6rem; }
}
</style>
