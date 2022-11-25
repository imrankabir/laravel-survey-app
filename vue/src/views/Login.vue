<template>
	<h1>Login</h1>
	<form @submit="login">
		<div v-if="errorMessage" class="alert alert-danger">
			{{ errorMessage }}
			<span @click="errorMessage = ''" class="">
				<svg xmlns="http://www.w3.org/2000/svg" style="width:20px;height:20px;" fill="none" viewBox="0 0 24 24" stroke="currentColor">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
				</svg>
			</span>
		</div>
		<div class="form-floating">
			<input type="email" class="form-control" id="email" v-model="user.email" placeholder="user@example.com">
			<label for="email">Email address</label>
		</div>
		<div class="form-floating">
			<input type="password" class="form-control" id="password" v-model="user.password" placeholder="Password">
			<label for="password">Password</label>
		</div>
		<div class="checkbox mb-3 float-left">
			<label>
				<input type="checkbox" value="remember-me" v-model="user.remember"> Remember me
			</label>
		</div>
		<button class="w-100 btn btn-lg btn-primary" type="submit"><span v-if="loading" class="spinner-border spinner-border-sm"></span> Login</button>
	</form>
</template>

<script setup>

import store from "../store";
import { useRouter } from "vue-router";
import { ref } from "vue";

const router = useRouter();

const user = {
	email: "",
	password: "",
	remember: false
};

const loading = ref(false);
const errorMessage = ref();

function login(e) {
	e.preventDefault();
	loading.value = true;
	store
		.dispatch("login", user)
		.then(() => {
			loading.value = false;
			router.push({
				name: "Dashboard",
			});
		})
		.catch((err) => {
			loading.value = false;
			errorMessage.value = err.response.data.error;
		});
}

</script>

<style scoped></style>