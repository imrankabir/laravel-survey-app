<template>
	<h4>Register</h4>
	<form @submit="register">
		<div v-if="errorMessage" class="alert alert-danger">
			{{ errorMessage }}
			<span @click="errorMessage = ''" class="">
				<svg xmlns="http://www.w3.org/2000/svg" style="width:20px;height:20px;" fill="none" viewBox="0 0 24 24" stroke="currentColor">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
				</svg>
			</span>
		</div>

		<div class="form-floating">
			<input type="text" class="form-control" id="name" v-model="user.name" placeholder="Your name">
			<label for="name">Name</label>
		</div>
		<div class="form-floating">
			<input type="email" class="form-control" id="email" v-model="user.email" placeholder="email@example.com">
			<label for="email">Email address</label>
		</div>
		<div class="form-floating">
			<input type="password" class="form-control" id="password" v-model="user.password" placeholder="Password">
			<label for="password">Password</label>
		</div>
		<div class="form-floating">
			<input type="password" class="form-control" id="password_confirmation" v-model="user.password_confirmation" placeholder="Password">
			<label for="password_confirmation">Password Confirmation</label>
		</div>
		<button class="w-100 btn btn-lg btn-primary" type="submit"><span v-if="loading" class="spinner-border spinner-border-sm"></span> Register</button>
	</form>
</template>

<script setup>

import store from "../store";
import { useRouter } from "vue-router";
import { ref } from "vue";

const router = useRouter();

const user = {
	name: "",
	email: "",
	password: "",
};

const loading = ref(false);
const errorMessage = ref();

function register(e) {
	e.preventDefault();
	loading.value = true;
	store
		.dispatch("register", user)
		.then(() => {
			loading.value = false;
			router.push({
				name: "Dashboard",
			});
		})
		.catch((error) => {
			loading.value = false;
			if (error.response.status === 422) {
				errorMessage.value = error.response.data.message;
			}
		});
}
</script>

<style scoped></style>