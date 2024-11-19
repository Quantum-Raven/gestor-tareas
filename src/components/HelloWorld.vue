<template>
  <div class="container mt-5 text-center">
    <br />
    <br />
    <h1 class="display-4 text-primary mb-4">Bienvenido a la Aplicación de Tareas con Vue</h1>
    <p>Esta aplicación te permite gestionar tus tareas de manera eficiente. Puedes añadir nuevas tareas manualmenteo
      extraerlas desde una API.</p>
    <br />
    <br />
    <br />
    <br />
    <h2 class="text-info mt-4">Secciones de la Aplicación</h2>
    <p class="lead text-muted"><strong>Añadir Tarea</strong>: Permite ingresar nuevas tareas manualmente.<br />
      <strong>Lista de Tareas</strong>: Muestra todas las tareas extraídas desde la API, permitiendo marcarlas
      como completadas o
      eliminarlas.<br />
      <strong>Vista Combinada</strong>: Combina las funcionalidades de añadir tareas manualmente y ver las tareas
      de la API al
      mismo tiempo.
    </p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>
