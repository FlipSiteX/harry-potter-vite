<template>
	<div
		@click="$emit('showFullCard', character)"
		class="bg-white hover:-translate-y-1 hover:shadow-lg hover:shadow-cyan-500/70 duration-150 rounded-lg flex cursor-pointer"
	>
		<img
			:src="
				character.image === '' ? '../src/assets/noPhoto.jpg' : character.image
			"
			alt="Character Image"
			class="object-cover w-48 h-full rounded-xl border-4 border-transparent"
		/>
		<div class="flex flex-1 justify-between p-4">
			<div>
				<h2 class="text-2xl font-semibold">{{ character.name }}</h2>
				<p class="text-gray-600 text-lg">
					{{ character.species }}, {{ character.gender }}
				</p>
				<div class="mt-4 text-lg">
					<p class="text-gray-700">
						<span class="font-semibold">House:</span> {{ character.house }}
					</p>
					<p class="text-gray-700">
						<span class="font-semibold">Date of Birth:</span>
						<span
							class="ml-1"
							v-if="character.dateOfBirth !== null"
						>
							{{ character.dateOfBirth }}
						</span>
						<span
							class="ml-1"
							v-else
						>
							{{ character.yearOfBirth }}
						</span>
					</p>
					<p class="text-gray-700">
						<span class="font-semibold">Patronus:</span>
						{{ character.patronus }}
					</p>
					<p class="text-gray-700">
						<span class="font-semibold">Alive:</span>
						{{ character.alive ? "Yes" : "No" }}
					</p>
					<p class="text-gray-700">
						<span class="font-semibold">Actor:</span> {{ character.actor }}
					</p>
				</div>
			</div>
			<div v-if="isAuth" class="ml-4">
				<i v-if="!bookmarkIsActive" @click.stop="bookmarkToggle(character)" class="fa-regular fa-bookmark text-2xl hover:text-yellow-400"></i>
				<i v-if="bookmarkIsActive" @click.stop="bookmarkToggle(character)" class="fa-solid fa-bookmark text-2xl text-yellow-400 hover:text-[#ff4242]"></i>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	emits: ['addFavourite', 'showFullCard'],
	props: {
		character: {
			type: Object,
			required: true,
		},
		isAuth: {	
			type: Boolean,
			required: true,
		}
	},
	data() {
		return {
			bookmarkIsActive: false,
		}
	},
	methods: {
		bookmarkToggle(character) {
			if (!this.bookmarkIsActive) {
				this.bookmarkIsActive = true
			} else {
				this.bookmarkIsActive = false
			}
			this.$emit('addFavourite', character)
		}
	}
};
</script>

<style></style>