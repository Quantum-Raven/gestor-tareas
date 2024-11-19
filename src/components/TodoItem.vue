<template>
    <div class="d-flex align-items-center p-2 border-bottom border-3">
        <div class="d-flex flex-column m-auto">
            <h4 class="title" :class="{ 'text-muted': completed, 'text-decoration-line-through': completed }">{{
                title }}</h4>

            <div class="container text-center">
                <span class="badge" :class="{ 'text-bg-success': completed, 'text-bg-warning': !completed }">
                    {{ completed ? "Completada" : "Pendiente" }}
                </span>
            </div>
        </div>
        <div class="d-flex flex-row">
            <button type="button" class="btn btn-sm m-1"
                :class="{ 'btn-outline-success': !completed, 'btn-outline-warning': completed }"
                @click="$emit('toggle-task-completion', id)">
                {{ completed ? 'Desmarcar' : 'Completar' }}
            </button>
            <button type="button" class="btn btn-outline-danger btn-sm m-1"
                @click="$emit('delete-task', id)">Eliminar</button>
        </div>
    </div>
    <!-- Contenedor principal del ítem de tarea -->
</template>

<script>
export default {
    // Define el nombre del componente
    name: 'TodoItem',

    // Define las propiedades que este componente recibirá del componente padre
    // Comentario: Puedes agregar más propiedades si es necesario (por ejemplo, 'dueDate' para la fecha de vencimiento)
    props: [
        'title',      // Título de la tarea
        'completed', // Estado de la tarea (completada o pendiente)
        'id'
    ]
}
</script>

<style scoped>
.title {
    font-size: 18px;
}


@media (min-width: 600px) {
    .title {
        font-size: 22px;
    }
}


@media (min-width: 992px) {
    .title {
        font-size: 24px;
    }
}

/* Puedes agregar tus propios estilos aquí */
/* Por ejemplo, cambia el color de fondo de las tareas completadas */
</style>