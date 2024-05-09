<template>
	<div class="max-w-2xl w-[90%] p-6 bg-white rounded-lg shadow-md">
		<h2 class="text-2xl font-semibold mb-4">Авторизация</h2>
		<form>
			<div class="flex gap-4">
				<div class="mb-4 flex-1">
					<TextInput
						v-model="login"
						:isCorrect="!login.match(/\S/g) && tryValidation"
						:type="'text'"
						:id="'login'"
						:placeholder="'Логин'"
					>
						Логин
					</TextInput>
					<p
						v-if="!login.match(/\S/g) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Заполните поле
					</p>
				</div>
				<div class="mb-4 flex-1">
					<TextInput
						v-model="password"
						:isCorrect="!password.match(/\S/g) && tryValidation"
						:type="'text'"
						:id="'password'"
						:placeholder="'Пароль'"
					>
						Пароль
					</TextInput>
					<p
						v-if="!password.match(/\S/g) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Заполните поле
					</p>
				</div>
			</div>

			<button
				@click="authorization"
				type="button"
				class="w-full mt-2 text-lg bg-indigo-500 text-white py-2 px-4 rounded-lg hover:bg-indigo-600 active:bg-indigo-500"
			>
				Войти
			</button>
		</form>
		<h2
			@click="$emit('showReg')"
			class="mt-4 w-max underline decoration-1 text-lg text-indigo-500 active:text-indigo-800 cursor-pointer"
		>
			Нет аккаунта? Регистрация
		</h2>
	</div>
</template>

<script>
import TextInput from "./TextInput.vue";
export default {
	emits: ['auth'],
	components: {
		TextInput,
	},
	data() {
		return {
			login: "",
			password: "",
			tryValidation: false,
		};
	},
	methods: {
		authorization() {
			this.tryValidation = true;
			if (this.login.match(/\S/g) && this.password.match(/\S/g)) {
				let keys = Object.keys(localStorage);
				for (let key of keys) {
					if (
						JSON.parse(localStorage[key]).login === this.login &&
						JSON.parse(localStorage[key]).password === this.password
					) {
						let user = JSON.parse(localStorage[key]);
						this.$emit('auth', user);
						return;
					}
				}
				alert('Пользователь не найден');
			}
		},
	},
};
</script>

<style></style>
