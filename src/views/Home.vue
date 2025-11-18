<script setup>
// Página inicial limpa — removidas referências ao sistema de gerenciamento de tarefas
</script>

<template>
  <section class="home-section">
    <div class="card">
      <div class="card-header">
        <h2>Bem-vindo</h2>
        <p class="subtitle">Esta é a página inicial. Conteúdo relacionado ao sistema de gerenciamento de tarefas foi removido.</p>
      </div>

      <div class="content">
        <p>Use a navegação para explorar o site.</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.home-section { display:flex; justify-content:center; padding:2rem 1rem; }
.card { background: white; border-radius: 12px; padding: 1.8rem; max-width:800px; width:100%; box-shadow: 0 8px 24px rgba(0,0,0,0.08); }
.card-header h2 { font-size:1.6rem; margin-bottom:0.5rem; }
.subtitle { color: #666; margin-bottom:1rem }
.content { color: #333 }
@media (max-width:768px){ .card { padding:1rem } }
</style>
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
