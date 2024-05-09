<template>
	<label
		:for="id"
		class="text-lg font-medium text-gray-700"
		>
        <slot></slot>
    </label>
	<input
		@mousedown="blockSpace($event.target)"
        @input="$emit('update:modelValue', $event.target.value)"
		:value="modelValue"
		class="mt-1 w-full outline-none text-lg font-medium border-2 rounded-lg p-2"
		:class="
			isCorrect
				? 'border-[#ff4242] focus:border-[#ff4242]'
				: 'border-slate-300 focus:border-slate-400'
		"
        :id
        :min
        :type
		:placeholder
	/>
</template>

<script>
export default {
    props: {
        modelValue: {
            type: String
        },
        id: {
            type: String,
            required: true
        },
        type: {
            type: String,
            required: true
        },
        placeholder: {
            type: String
        },
        isCorrect: {
            type: Boolean
        },
        min: {
            type: Number
        }
    },
    methods: {
        blockSpace(input) {
			input.onkeydown = (event) => {
				if (event.code == 'Space') {
					return false
				}
			}
		},
    }
}
</script>

<style>
</style>