<template>

	<header class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0 shadow">
		<router-link class="navbar-brand col-md-3 col-lg-2 me-0 px-3 fs-6" to="/">Survey App</router-link>
		<div class="navbar-nav">
			<div class="nav-item text-nowrap d-flex">
				<router-link class="nav-link px-3" to="/register">Register</router-link>
				<router-link class="nav-link px-3" to="/login">Login</router-link>
			</div>
		</div>
	</header>

	<router-view></router-view>
	
</template>

<script>
export default {
	name: "AuthLayout"
}
</script>

<style scoped>

</style>