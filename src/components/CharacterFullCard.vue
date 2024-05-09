<template>
	<div
		class="bg-white w-[900px] h-[80vh] shadow-xl overflow-hidden rounded-lg flex"
	>
		<div
			class="w-1/2 h-full border-4 border-transparent overflow-hidden rounded-xl"
		>
			<img
				:src="character.image === '' ? '../src/assets/noPhoto.jpg' : character.image"
				alt="Character Image"
				class="object-cover w-full h-full"
			/>
		</div>
		<div
			class="flex flex-col text-xl flex-1 overflow-y-scroll justify-between my-2 p-4"
		>
			<h2 class="text-4xl font-semibold">{{ character.name }}</h2>
			<p
				v-if="character.hogwartsStudent"
				class="font-semibold text-xl text-gray-800 mt-4"
			>
				Hogwarts Student
			</p>
			<p
				v-if="character.hogwartsStaff"
				class="font-semibold text-xl text-gray-800 mt-4"
			>
				Hogwarts Staff
			</p>
			<p
				v-if="character.alternate_names.length > 0"
				class="text-xl text-gray-800 mt-4"
			>
				<span class="text-xl font-semibold"> Alternate names: </span>
				{{ character.alternate_names.join(', ') }}
			</p>
			<p class="text-gray-800 mt-4">
				<span class="font-semibold">House:</span> {{ character.house }}
			</p>
			<p class="text-gray-800 mt-4">
				<span class="font-semibold">Species:</span> {{ character.species }}
			</p>
			<p class="text-gray-800 mt-4">
				<span class="font-semibold">Gender:</span> {{ character.gender }}
			</p>
			<p class="text-gray-800 mt-4">
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
			<p class="text-gray-800 mt-4">
				<span class="font-semibold">Eye colour:</span>
				{{ character.eyeColour }}
			</p>
			<p class="text-gray-800 mt-4">
				<span class="font-semibold">Hair colour:</span>
				{{ character.hairColour }}
			</p>
			<p class="text-gray-800 mt-4">
				<span class="font-semibold">Ancestry:</span>
				{{ character.ancestry }}
			</p>
			<p class="text-gray-800 mt-4">
				<span class="font-semibold">Wizard:</span>
				{{ character.wizard ? 'Yes' : 'No' }}
			</p>
			<p class="text-gray-800 mt-4">
				<span class="font-semibold">Patronus:</span>
				{{ character.patronus }}
			</p>
			<div class="flex mt-4">
				<p class="text-gray-800 font-semibold">Wand:</p>
				<div class="ml-4 text-gray-800">
					<p>Wood: {{ character.wand['wood'] }}</p>
					<p>Core: {{ character.wand['core'] }}</p>
					<p>Length: {{ character.wand['length'] }}</p>
				</div>
			</div>
			<p class="text-gray-800 mt-4">
				<span class="font-semibold">Alive:</span>
				{{ character.alive ? 'Yes' : 'No' }}
			</p>
			<p class="text-gray-800 mt-4">
				<span class="font-semibold">Actor:</span> {{ character.actor }}
			</p>
			<p
				v-if="character.alternate_actors.length > 0"
				class="text-gray-800 mt-4"
			>
				<span class="font-semibold">Alternate Actors:</span>
				{{ character.alternate_actors.join(', ') }}
			</p>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		character: {
			type: Object,
			required: true,
		},
	},
};
</script>

<style></style>
