<template>
	<select
    @change="$emit('update:modelValue', $event.target.value)"
		class="text-xl outline-none bg-slate-600/50 text-white focus:border-slate-300 font-medium border-2 border-slate-400 rounded-lg py-2.5 px-2"
	>
		<option
			disabled
			selected
			class="text-black"
		>
			<slot></slot>
		</option>
		<option
			v-for="option in options"
			:value="option.value"
		>
			{{ option.text }}
		</option>
	</select>
</template>

<script>
export default {
	props: {
		options: {
			type: Array,
			required: true,
		},
        modelValue: {
            type: String
        }
	},
};
</script>

<style></style>
