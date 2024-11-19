<script setup>
import TodoItem from '@/components/TodoItem.vue';
</script>

<template>
    <div class="container p-2 m-auto">
        <h1>Lista de Tareas</h1>
        <button @click="fetchTasks" class="btn btn-primary btn-sm">Cargar Tareas</button>
        <div v-if="tasks.length > 0" class="mt-4">
            <div v-for="task in tasks" :key="task.id">
                <TodoItem :id="task.id" :title="task.todo" v-bind:completed="task.completed"
                    @toggle-task-completion="toggleTaskCompletion" @delete-task="deleteTask" />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "TaskList",
    data() {
        return {
            tasks: [], // Almacenamiento local de las tareas traídas de la API
        };
    },
    methods: {
        // Llamada para obtener las tareas desde la API externa
        fetchTasks() {
            fetch("https://dummyjson.com/todos")
                .then(res => res.json())
                .then(data => {
                    this.tasks = data.todos;
                });
        },
        // Cambiar el estado de una tarea (completada/no completada)
        toggleTaskCompletion(taskId) {
            let changedIndex = this.tasks.findIndex(t => t.id === taskId);
            this.tasks[changedIndex].completed = !this.tasks[changedIndex].completed;
            this.tasks = [...this.tasks];
        },
        // Eliminar la tarea seleccionada
        deleteTask(taskId) {
            this.tasks = this.tasks.filter((t) => t.id !== taskId);
        }
    },
};
</script>
