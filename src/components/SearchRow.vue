<template>
	<label class="relative block">
		<span class="absolute z-[1] inset-y-0 left-0 flex items-center pl-2">
			<i class="fa-solid fa-magnifying-glass text-slate-300 ml-2"></i>
		</span>
		<input
			class="h-full w-full pl-10 pr-4 text-xl placeholder:text-slate-300 outline-none bg-slate-600/50 text-white focus:border-slate-300 font-medium border-2 border-slate-400 rounded-lg"
			placeholder="Поиск..."
			type="text"
			@input="$emit('update:modelValue', $event.target.value)"
		/>
	</label>
</template>

<script>
export default {
	props: {
		modelValue: {
			type: String
		}
	}
};
</script>

<style scoped></style>
