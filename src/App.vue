<template>
  <div id="app" class="container">
    <h1 class="title">To-Do List</h1>

    <!-- Formulaire pour ajouter une tâche -->
    <form @submit.prevent="addTask" class="task-form">
      <input v-model="newTask" placeholder="Nouvelle tâche" class="input-task"/>
      <button type="submit" class="btn-add">Ajouter</button>
    </form>

    <!-- Liste des tâches -->
    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        <span :class="{ completed: task.completed }" class="task-name">{{ task.name }}</span>
        <div class="task-actions">
          <button @click="toggleTask(index)" class="btn-complete">
            {{ task.completed ? 'Reprendre' : 'Terminer' }}
          </button>
          <button @click="removeTask(index)" class="btn-delete">Supprimer</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '', // Nouvelle tâche
      tasks: [],  // Liste des tâches
    };
  },
  methods: {
    // Ajouter une nouvelle tâche
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ name: this.newTask, completed: false }); // Ajoute la tâche
        this.newTask = ''; // Vide le champ d'entrée après l'ajout
      }
    },
    // Supprimer une tâche
    removeTask(index) {
      this.tasks.splice(index, 1); // Supprime la tâche de la liste
    },
    // Marquer une tâche comme terminée ou non
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed; // Inverse l'état de la tâche (terminée ou non)
    },
  },
};
</script>

<style scoped>
/* Mise en page de l'application */
.container {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  font-family: Arial, sans-serif;
}

.title {
  text-align: center;
  color: #333;
  font-size: 2em;
  margin-bottom: 20px;
}

/* Style du formulaire */
.task-form {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.input-task {
  flex: 1;
  padding: 10px;
  font-size: 1em;
  border: 2px solid #ddd;
  border-radius: 4px;
  margin-right: 10px;
}

.btn-add {
  background-color: #28a745;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn-add:hover {
  background-color: #218838;
}

/* Liste de tâches */
.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 4px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}

.task-name {
  font-size: 1.2em;
  color: #333;
}

.task-actions {
  display: flex;
  gap: 10px;
}

/* Boutons pour terminer et supprimer */
.btn-complete {
  background-color: #ffc107;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}

.btn-complete:hover {
  background-color: #e0a800;
}

.btn-delete {
  background-color: #dc3545;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}

.btn-delete:hover {
  background-color: #c82333;
}

/* Style pour les tâches terminées */
.completed {
  text-decoration: line-through;
  color: #aaa;
}
</style>
