<script setup>
import TodoItem from '@/components/TodoItem.vue';
</script>

<template>
    <div class="container p-2 m-auto">
        <h1>Vista Combinada</h1>
        <div class="row justify-content-center">
            <div class="col-6">
                <input v-model="newTask" @keyup.enter="addTask" placeholder="Añadir nueva tarea" class="form-control" />
            </div>
            <div class="col-auto">
                <button @click="addTask" class="btn btn-primary m-1">Añadir</button>
            </div>
        </div>
        <div v-if="tasks.length > 0" class="mt-4">
            <div v-for="task in tasks" :key="task.id">
                <TodoItem :id="task.id" :title="task.todo" v-bind:completed="task.completed"
                    @toggle-task-completion="toggleTaskCompletion" @delete-task="deleteTask" />
            </div>
        </div>
    </div>
</template>

<script>
// Esta sección debe permitir agregar tareas nuevas a la vez que extraer las tareas anteriores de la API
export default {
    name: "CombinedView",
    data() {
        return {
            newTask: "",
            tasks: []
        }
    },
    beforeMount() {
        fetch("https://dummyjson.com/todos")
            .then(res => res.json())
            .then(data => {
                this.tasks = data.todos;
            });
    },
    methods: {
        addTask() {
            if (this.newTask.trim() === "") return;

            const newTask = {
                todo: this.newTask,
                completed: false,
                id: Date.now(),
            };

            // Añadir la nueva tarea al inicio de la lista
            this.tasks.unshift(newTask);
            this.newTask = ""; // Limpiar el campo de entrada después de agregar
        },

        // Elimina una tarea específica de la lista
        deleteTask(taskId) {
            this.tasks = this.tasks.filter((t) => t.id !== taskId);
        },

        // Cambia el estado de la tarea entre completada y no completada
        toggleTaskCompletion(taskId) {
            let changedIndex = this.tasks.findIndex(t => t.id === taskId);
            this.tasks[changedIndex].completed = !this.tasks[changedIndex].completed;
            this.tasks = [...this.tasks];


        },
    }
}

</script>