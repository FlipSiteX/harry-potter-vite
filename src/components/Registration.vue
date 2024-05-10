<template>
	<div class="max-w-2xl w-[90%] p-6 bg-white rounded-lg shadow-md">
		<h2 class="text-2xl font-semibold mb-4">Регистрация</h2>
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
						:type="'password'"
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

			<div class="flex gap-4 mb-4">
				<div class="flex-1">
					<TextInput
						v-model="firstName"
						:isCorrect="
							(!firstName.match(/\S/g) ||
								firstName.match(/^[а-яё]/) ||
								firstName.match(/^[А-ЯЁ].*[А-ЯЁ].*/g) ||
								!firstName.match(/^[А-ЯЁ][а-яё]*$/gi) ||
								firstName.match(/^[А-ЯЁ]$/)) &&
							tryValidation
						"
						:type="'text'"
						:id="'firstName'"
						:placeholder="'Иван'"
					>
						Имя
					</TextInput>
					<p
						v-if="!firstName.match(/\S/g) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Заполните поле
					</p>
					<p
						v-else-if="firstName.match(/^[а-яё]/) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Первая буква должна быть заглавной
					</p>
					<p
						v-else-if="firstName.match(/^[А-ЯЁ].*[А-ЯЁ].*/g) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Только первая буква может быть заглавной
					</p>
					<p
						v-else-if="!firstName.match(/^[А-ЯЁ][а-яё]*$/gi) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Используйте только русские буквы
					</p>
					<p
						v-else-if="firstName.match(/^[А-ЯЁ]$/) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Используйте минимум 2 буквы
					</p>
				</div>
				<div class="flex-1">
					<TextInput
						v-model="lastName"
						:isCorrect="
							(!lastName.match(/\S/g) ||
								lastName.match(/^[а-яё]/) ||
								lastName.match(/^[А-ЯЁ].*[А-ЯЁ].*/g) ||
								lastName.match(/^[А-ЯЁ]$/) ||
								lastName.match(/^[А-ЯЁ][а-яё]$/) ||
								!lastName.match(/^[А-ЯЁ][а-яё]*$/gi)) &&
							tryValidation
						"
						:type="'text'"
						:id="'lastName'"
						:placeholder="'Иванов'"
					>
						Фамилия
					</TextInput>
					<p
						v-if="!lastName.match(/\S/g) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Заполните поле
					</p>
					<p
						v-else-if="lastName.match(/^[а-яё]/) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Первая буква должна быть заглавной
					</p>
					<p
						v-else-if="lastName.match(/^[А-ЯЁ].*[А-ЯЁ].*/g) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Только первая буква может быть заглавной
					</p>
					<p
						v-else-if="
							(lastName.match(/^[А-ЯЁ]$/) && tryValidation) ||
							(lastName.match(/^[А-ЯЁ][а-яё]$/) && tryValidation)
						"
						class="mt-1 text-[#ff4242]"
					>
						Используйте минимум 3 буквы
					</p>
					<p
						v-else-if="!lastName.match(/^[А-ЯЁ][а-яё]*$/gi) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Используйте только русские буквы
					</p>
				</div>
				<div class="flex-1">
					<TextInput
						v-model="patronymic"
						:isCorrect="
							(!patronymic.match(/\S/g) ||
								patronymic.match(/^[а-яё]/) ||
								patronymic.match(/^[А-ЯЁ].*[А-ЯЁ].*/g) ||
								patronymic.match(/^[А-ЯЁ]$/) ||
								patronymic.match(/^[А-ЯЁ][а-яё]$/) ||
								!patronymic.match(/^[А-ЯЁ][а-яё]*$/gi)) &&
							tryValidation
						"
						:type="'text'"
						:id="'patronymic'"
						:placeholder="'Иванович'"
					>
						Отчество
					</TextInput>
					<p
						v-if="!patronymic.match(/\S/g) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Заполните поле
					</p>
					<p
						v-else-if="patronymic.match(/^[а-яё]/) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Первая буква должна быть заглавной
					</p>
					<p
						v-else-if="patronymic.match(/^[А-ЯЁ].*[А-ЯЁ].*/g) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Только первая буква может быть заглавной
					</p>
					<p
						v-else-if="
							(patronymic.match(/^[А-ЯЁ]$/) && tryValidation) ||
							(patronymic.match(/^[А-ЯЁ][а-яё]$/) && tryValidation)
						"
						class="mt-1 text-[#ff4242]"
					>
						Используйте минимум 3 буквы
					</p>
					<p
						v-else-if="!patronymic.match(/^[А-ЯЁ][а-яё]*$/gi) && tryValidation"
						class="mt-1 text-[#ff4242]"
					>
						Используйте только русские буквы
					</p>
				</div>
			</div>

			<div class="mb-4 gap-4 flex">
				<div class="flex-1">
					<TextInput
						v-model="phone"
						:isCorrect="
							!/^8\([0-9][0-9][0-9]\)[0-9][0-9][0-9]\-[0-9][0-9]\-[0-9][0-9]$/.test(
								phone
							) && tryValidation
						"
						:type="'text'"
						:id="'phone'"
						:placeholder="'8(ХХХ)ХХХ-ХХ-ХХ'"
					>
						Номер телефона
					</TextInput>
					<p
						v-if="
							!/^8\([0-9][0-9][0-9]\)[0-9][0-9][0-9]\-[0-9][0-9]\-[0-9][0-9]$/.test(
								phone
							) && tryValidation
						"
						class="mt-1 text-[#ff4242] flex flex-col"
					>
						<span>Укажите телефон в формате:</span>8(123)456-78-90
					</p>
				</div>
				<div class="flex-1">
					<TextInput
						v-model="age"
						:isCorrect="age < 10 && tryValidation"
						:type="'number'"
						:min="10"
						:id="'age'"
					>
						Возраст
					</TextInput>
					<p
						v-if="age < 10 && tryValidation"
						class="mt-1 text-[#ff4242] flex flex-col"
					>
						Не менее 10 лет
					</p>
				</div>
			</div>

			<div class="mb-4 flex">
				<div class="flex flex-col">
					<label class="text-lg font-medium text-gray-700">Пол</label>
					<div class="mt-1">
						<label class="inline-flex items-center">
							<input
								type="radio"
								v-model="gender"
								name="gender"
								value="male"
								class="form-radio h-4 w-4"
							/>
							<span class="ml-2 text-lg">Мужской</span>
						</label>
						<label class="inline-flex items-center ml-6">
							<input
								type="radio"
								v-model="gender"
								name="gender"
								value="female"
								class="form-radio h-4 w-4"
							/>
							<span class="ml-2 text-lg">Женский</span>
						</label>
					</div>
				</div>
			</div>

			<div class="mb-4">
				<label class="text-lg font-medium text-gray-700"
					>Любимый факультет в Хогвартсе</label
				>
				<div class="mt-1 flex gap-x-4">
					<label class="flex items-center">
						<input
							type="checkbox"
							v-model="favoriteFaculty"
							value="Gryffindor"
							class="form-checkbox h-4 w-4"
						/>
						<span class="ml-2 text-lg">Гриффиндор</span>
					</label>
					<label class="flex items-center">
						<input
							type="checkbox"
							v-model="favoriteFaculty"
							value="Ravenclaw"
							class="form-checkbox h-4 w-4"
						/>
						<span class="ml-2 text-lg">Когтевран</span>
					</label>
					<label class="flex items-center">
						<input
							type="checkbox"
							v-model="favoriteFaculty"
							value="Hufflepuff"
							class="form-checkbox h-4 w-4"
						/>
						<span class="ml-2 text-lg">Пуффендуй</span>
					</label>
					<label class="flex items-center">
						<input
							type="checkbox"
							v-model="favoriteFaculty"
							value="Slytherin"
							class="form-checkbox h-4 w-4"
						/>
						<span class="ml-2 text-lg">Слизерин</span>
					</label>
				</div>
			</div>
			<button
				@click="registration"
				type="button"
				class="w-full mt-2 text-lg bg-indigo-500 text-white py-2 px-4 rounded-lg hover:bg-indigo-600 active:bg-indigo-500"
			>
				Зарегистрироваться
			</button>
		</form>
		<h2
			@click="$emit('showAuth')"
			class="mt-4 w-max underline decoration-1 text-lg text-indigo-500 active:text-indigo-800 cursor-pointer"
		>
			Уже есть аккаунт? Авторизация
		</h2>
	</div>
</template>

<script>
import TextInput from "./TextInput.vue";
export default {
	emits: ["auth"],
	components: {
		TextInput,
	},
	data() {
		return {
			login: "",
			password: "",
			firstName: "",
			lastName: "",
			patronymic: "",
			phone: "",
			age: "",
			gender: "male",
			favoriteFaculty: [],
			tryValidation: false,
		};
	},
	methods: {
		registration() {
			this.tryValidation = true;
			if (
				this.login.match(/\S/g) &&
				this.password.match(/\S/g) &&
				this.firstName.match(/\S/g) &&
				!this.firstName.match(/^[а-яё]/) &&
				!this.firstName.match(/^[А-ЯЁ].*[А-ЯЁ].*/g) &&
				this.firstName.match(/^[А-ЯЁ][а-яё]*$/gi) &&
				!this.firstName.match(/^[А-ЯЁ]$/) &&
				this.lastName.match(/\S/g) &&
				!this.lastName.match(/^[а-яё]/) &&
				!this.lastName.match(/^[А-ЯЁ].*[А-ЯЁ].*/g) &&
				this.lastName.match(/^[А-ЯЁ][а-яё]*$/gi) &&
				!this.lastName.match(/^[А-ЯЁ]$/) &&
				!this.lastName.match(/^[А-ЯЁ][а-яё]$/) &&
				this.patronymic.match(/\S/g) &&
				!this.patronymic.match(/^[а-яё]/) &&
				!this.patronymic.match(/^[А-ЯЁ].*[А-ЯЁ].*/g) &&
				this.patronymic.match(/^[А-ЯЁ][а-яё]*$/gi) &&
				!this.patronymic.match(/^[А-ЯЁ]$/) &&
				!this.patronymic.match(/^[А-ЯЁ][а-яё]$/) &&
				/^8\([0-9][0-9][0-9]\)[0-9][0-9][0-9]\-[0-9][0-9]\-[0-9][0-9]$/.test(
					this.phone
				) &&
				this.age >= 10
			) {
				let key = Date.now();
				let user = {
					login: this.login,
					password: this.password,
					firstName: this.firstName,
					lastName: this.lastName,
					patronymic: this.patronymic,
					phone: this.phone,
					age: this.age,
					gender: this.gender,
					favoriteFaculty: this.favoriteFaculty,
				};
				if (this.isUserExist) {
					alert('Пользователь с данным логином уже существует');
				} else {
					localStorage.setItem(key, JSON.stringify(user));
					this.$emit("auth", user);
				}
			}
		},
	},
	computed: {
		isUserExist() {
			let keys = Object.keys(localStorage);
			for (let key of keys) {
				if (
					JSON.parse(localStorage[key]).login === this.login &&
					JSON.parse(localStorage[key]).password === this.password
				) {
					return true;
				}
			}
			return false;
		},
	},
};
</script>

<style></style>
