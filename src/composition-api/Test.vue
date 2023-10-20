<script setup>
	import {
		defineProps
	} from 'vue';
	const props = defineProps({
		demo: {
			type: String,
			default: 'neida'
		}
	})
	const hey = 'Hallo'

</script>

<template>
	<div>
		{{hey}}
		{{props.demo}}
	</div>
</template>