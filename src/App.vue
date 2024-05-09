<template>
	<section class="mt-4 px-6 flex w-full justify-between">
		<section class="max-w-6xl flex-1 mr-10">
			<div class="flex gap-x-4 mb-4">
				<SearchRow
					class="w-1/2"
					v-model="searchTerm"
				/>
				<OptionsSelect
					:options="sortOptions"
					v-model="selectedSort"
					class="w-1/2"
				>
					Выберите сортировку
				</OptionsSelect>
			</div>

			<div class="flex gap-x-4 mb-2">
				<OptionsSelect
					:options="houseFilterOptions"
					v-model="houseFilter"
					class="w-1/2"
				>
					Фильтрация по факультету
				</OptionsSelect>
				<OptionsSelect
					:options="speciesFilterOptions"
					v-model="speciesFilter"
					class="w-1/2"
				>
					Фильтрация по виду
				</OptionsSelect>
			</div>

			<div
				class="grid auto-rows-max grid-cols-1 2xl:grid-cols-2 gap-y-4 gap-x-2 py-2 overflow-y-scroll h-[800px]"
			>
				<CharacterShortCard
					v-for="character in searchCharacters"
					:key="character.id"
					:isAuth
					:character
					@showFullCard="showFullCard"
					@addFavourite="addFavourite"
					class="mr-2"
				/>
			</div>
		</section>

		<div class="flex flex-col text-end">
			<button
				v-if="!currentUser"
				class="text-white h-max text-xl bg-slate-600/50 hover:border-slate-300 font-medium border-2 border-slate-400 rounded-lg py-2.5 px-8 mb-4"
				@click="showAuth"
			>
				Авторизация
			</button>

			<h2
				v-if="currentUser"
				class="text-white text-2xl font-semibold mb-4"
			>
				{{ currentUser.lastName }} {{ currentUser.firstName }} {{ currentUser.patronymic }}
			</h2>

			<div class="flex flex-col items-end" v-if="currentUser">
				<h2 class="text-white text-xl font-semibold">Избранное</h2>
				<table class="text-white text-xl mt-4">
					<tr>
						<td class="border-2 border-slate-400">Волшебники</td>
						<td class="border-2 border-slate-400">Не волшебники</td>
					</tr>
					<tr>
						<td class="border-2 border-slate-400">
							{{ favouritesCharacters.filter((c) => c.wizard).length }}
						</td>
						<td class="border-2 border-slate-400">
							{{ favouritesCharacters.filter((c) => !c.wizard).length }}
						</td>
					</tr>
				</table>
			</div>
		</div>
	</section>

	<ModalWindow
		:showModal
		@closeModal="showModal = false"
	>
		<component
			:character="selectedCharacter"
			@showReg="showReg"
			@showAuth="showAuth"
			@auth="auth"
			:is="modalComp"
		></component>
	</ModalWindow>
</template>

<script>
import CharacterShortCard from "./components/CharacterShortCard.vue";
import CharacterFullCard from "./components/CharacterFullCard.vue";
import SearchRow from "./components/SearchRow.vue";
import OptionsSelect from "./components/OptionsSelect.vue";
import ModalWindow from "./components/ModalWindow.vue";
import Registration from "./components/Registration.vue";
import Authorization from "./components/Authorization.vue";
export default {
	components: {
		CharacterShortCard,
		CharacterFullCard,
		SearchRow,
		OptionsSelect,
		ModalWindow,
		Registration,
		Authorization,
	},
	data() {
		return {
			characters: [],
			modalComp: null,
			searchTerm: "",
			sortOptions: [
				{ value: "", text: "Без сортировки" },
				{ value: "nameUp", text: "По имени персонажа (A-Z)" },
				{ value: "nameDown", text: "По имени персонажа (Z-A)" },
				{ value: "actorNameUp", text: "По имени актёра (A-Z)" },
				{ value: "actorNameDown", text: "По имени актёра (Z-A)" },
				{ value: "ageDown", text: "По году рождения (От позднего)" },
				{ value: "ageUp", text: "По году рождения (От раннего)" },
			],
			houseFilterOptions: [
				{ value: "", text: "Без фильтрации" },
				{ value: "Gryffindor", text: "Gryffindor" },
				{ value: "Slytherin", text: "Slytherin" },
				{ value: "Hufflepuff", text: "Hufflepuff" },
				{ value: "Ravenclaw", text: "Ravenclaw" },
			],
			speciesFilterOptions: [
				{ value: "", text: "Без фильтрации" },
				{ value: "human", text: "human" },
				{ value: "half-giant", text: "half-giant" },
				{ value: "goblin", text: "goblin" },
				{ value: "werewolf", text: "werewolf" },
				{ value: "poltergeist", text: "poltergeist" },
				{ value: "ghost", text: "ghost" },
				{ value: "dragon", text: "dragon" },
				{ value: "centaur", text: "centaur" },
				{ value: "house-elf", text: "house-elf" },
				{ value: "acromantula", text: "acromantula" },
				{ value: "hippogriff", text: "hippogriff" },
				{ value: "giant", text: "giant" },
				{ value: "vampire", text: "vampire" },
				{ value: "owl", text: "owl" },
			],
			selectedSort: "",
			houseFilter: "",
			speciesFilter: "",
			showModal: false,
			selectedCharacter: "",
			isAuth: false,
			currentUser: "",
			favouritesCharacters: [],
		};
	},
	methods: {
		async fetchCharacters() {
			const rez = await fetch("https://hp-api.onrender.com/api/characters");
			this.characters = await rez.json();
		},
		splitArray(array, elField, filterOption) {
			let arr1 = array.filter((el) => el[elField] !== filterOption);
			let arr2 = array.filter((el) => el[elField] === filterOption);
			arr1.push(...arr2);
			return arr1;
		},
		showFullCard(character) {
			this.showModal = true;
			this.modalComp = CharacterFullCard;
			this.selectedCharacter = character;
		},
		showAuth() {
			this.showModal = true;
			this.modalComp = Authorization;
		},
		showReg() {
			this.modalComp = Registration;
		},
		auth(user) {
			this.showModal = false;
			this.isAuth = true;
			this.currentUser = user;
		},
		addFavourite(character) {
			if (!this.favouritesCharacters.includes(character)) {
				this.favouritesCharacters.push(character);
			} else {
				this.favouritesCharacters = this.favouritesCharacters.filter((c) => c !== character)
			}
		},
	},
	computed: {
		sortCharacters() {
			if (this.selectedSort === "ageUp") {
				return this.splitArray([...this.characters], "yearOfBirth", null).sort(
					(a, b) =>
						a.yearOfBirth === null || b.yearOfBirth === null
							? 1
							: a.yearOfBirth - b.yearOfBirth
				);
			} else if (this.selectedSort === "ageDown") {
				return this.splitArray([...this.characters], "yearOfBirth", null).sort(
					(a, b) =>
						a.yearOfBirth === null || b.yearOfBirth === null
							? 1
							: b.yearOfBirth - a.yearOfBirth
				);
			} else if (this.selectedSort === "nameUp") {
				return [...this.characters].sort((a, b) =>
					a["name"].localeCompare(b["name"])
				);
			} else if (this.selectedSort === "nameDown") {
				return [...this.characters].sort((a, b) =>
					b["name"].localeCompare(a["name"])
				);
			} else if (this.selectedSort === "actorNameUp") {
				return this.splitArray([...this.characters], "actor", "").sort((a, b) =>
					a["actor"] == "" || b["actor"] == ""
						? 1
						: a["actor"].localeCompare(b["actor"])
				);
			} else if (this.selectedSort === "actorNameDown") {
				return this.splitArray([...this.characters], "actor", "").sort((a, b) =>
					a["actor"] == "" || b["actor"] == ""
						? 1
						: b["actor"].localeCompare(a["actor"])
				);
			}
			return [...this.characters];
		},
		houseFilterCharacters() {
			if (
				["Gryffindor", "Slytherin", "Hufflepuff", "Ravenclaw"].includes(
					this.houseFilter
				)
			) {
				return this.sortCharacters.filter(
					(character) => character.house === this.houseFilter
				);
			}
			return this.sortCharacters;
		},
		speciesFilterCharacters() {
			if (
				[
					"human",
					"half-giant",
					"goblin",
					"werewolf",
					"poltergeist",
					"ghost",
					"dragon",
					"centaur",
					"house-elf",
					"acromantula",
					"hippogriff",
					"giant",
					"vampire",
					"owl",
				].includes(this.speciesFilter)
			) {
				return this.houseFilterCharacters.filter(
					(character) => character.species === this.speciesFilter
				);
			}
			return this.houseFilterCharacters;
		},
		searchCharacters() {
			return this.speciesFilterCharacters.filter(
				(el) =>
					el.name.toLowerCase().includes(this.searchTerm.toLowerCase()) ||
					el.actor.toLowerCase().includes(this.searchTerm.toLowerCase()) ||
					el.house.toLowerCase().includes(this.searchTerm.toLowerCase())
			);
		},
	},
	mounted() {
		this.fetchCharacters();
	},
};
</script>

<style scoped>
td {
	padding: 4px 8px;
}
</style>
