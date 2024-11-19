<template>
	<div id="app">
		<!-- Barra de navegación con enlaces a diferentes rutas -->
		<div class="mobile-menu" :class="{ 'mobile-menu-hidden': !isMenuActive }">
			<router-link class="dropdown-item text-white fs-5 p-2" to="/addtask">Agregar Tarea</router-link>
			<router-link class="dropdown-item text-white fs-5 p-2" to="/tasklist">Lista de Tareas</router-link>
			<router-link class="dropdown-item text-white fs-5 p-2" to="/combined">Vista Combinada</router-link>
		</div>
		<nav class="general-nav navbar navbar-expand-lg navbar-dark bg-primary shadow-sm">
			<div class="container">
				<router-link class="navbar-brand fs-5" to="/">Home</router-link>

				<button @click="() => { this.isMenuActive = !this.isMenuActive }" id="menu-btn"
					class="btn btn-secondary navbar-toggler dropdown-toggle" type="button" data-bs-toggle="dropdown"
					aria-expanded="false">
					<i class="navbar-toggler-icon" />
				</button>
			</div>

			<div class="collapse navbar-collapse">
				<router-link class="navbar-brand fs-6" to="/addtask">Agregar Tarea</router-link>
				<router-link class="navbar-brand fs-6" to="/tasklist">Lista de Tareas</router-link>
				<router-link class="navbar-brand fs-6" to="/combined">Vista Combinada</router-link>
			</div>
		</nav>
		<!-- Aquí se cargará el componente correspondiente a la ruta seleccionada -->
		<router-view />
	</div>
</template>

<script>
export default {
	data() {
		return {
			isMenuActive: false
		}
	}
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
}

.general-nav {
	z-index: 2;
}

.mobile-menu {
	position: fixed;
	top: 56px;
	background-color: #0d6efd;
	width: 100vw;
	height: calc(35vh - 56px);
	z-index: 1;
	transition: 200ms;
}

.mobile-menu-hidden {
	top: -1920px;
}


@media (min-width: 992px) {
	.mobile-menu {
		display: none;
	}
}
</style>
