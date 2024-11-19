<template>
    <div class="container p-2 m-auto">
        <h1>Añadir Tarea</h1>
        <div class="row justify-content-center">
            <div class="col-6">
                <input v-model="newTask" @keyup.enter="addTask" placeholder="Añadir nueva tarea" class="form-control" />
            </div>
            <div class="col-auto">
                <button @click="addTask" class="btn btn-primary">Añadir</button>
            </div>
        </div>

        <div v-if="tasks.length > 0" class="mt-4">
            <div v-for="task in tasks" :key="task.id" class="d-flex align-items-center p-2 border-bottom border-3">
                <div class="d-flex flex-column m-auto">
                    <h4 class="h4"
                        :class="{ 'text-muted': task.completed, 'text-decoration-line-through': task.completed }">{{
                            task.todo }}</h4>

                    <div class="container text-center">
                        <span class="badge"
                            :class="{ 'text-bg-success': task.completed, 'text-bg-warning': !task.completed }">
                            {{ task.completed ? "Completada" : "Pendiente" }}
                        </span>
                    </div>
                </div>
                <div class="d-flex flex-row">
                    <button type="button" class="btn btn-sm m-1"
                        :class="{ 'btn-outline-success': !task.completed, 'btn-outline-warning': task.completed }"
                        @click="toggleTaskCompletion(task)">
                        {{ task.completed ? 'Desmarcar' : 'Completar' }}
                    </button>
                    <button type="button" class="btn btn-outline-danger btn-sm m-1"
                        @click="deleteTask(task)">Eliminar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "AddTask",
    data() {
        return {
            newTask: "", // Campo de entrada para la nueva tarea
            tasks: [],   // Lista de tareas locales
        };
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
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },

        // Cambia el estado de la tarea entre completada y no completada
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },
    },
};
</script>