<template>

	<header class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0 shadow">
		<router-link class="navbar-brand col-md-3 col-lg-2 me-0 px-3 fs-6" to="/">Survey App</router-link>
		<div class="navbar-nav">
			<div class="nav-item text-nowrap">
				<a class="nav-link px-3" @click="logout">Logout</a>
			</div>
		</div>
	</header>

	<router-view></router-view>

</template>

<script>

import { useStore } from "vuex";
import { computed } from "vue";
import { useRouter } from "vue-router";

const navigation = [
	{ name: "Dashboard", to: { name: "Dashboard" } },
];

export default {

	setup() {
	
		const store = useStore();
		const router = useRouter();

		function logout() {
			store.dispatch("logout").then(() => {
				router.push({
					name: "Login",
				});
			});
		}

		store.dispatch("getUser");

		return {
			user: computed(() => store.state.user.data),
			navigation,
			logout,
		};

	}
}

</script>

<style scoped>

</style>