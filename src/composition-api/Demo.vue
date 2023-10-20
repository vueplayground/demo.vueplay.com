<template>
	<div>
		{{hey}}
		<Test demo="So Whats up" />
		<comp />
		<banana />
	</div>
</template>
<script setup>
	import {
		defineProps
	} from 'vue';
	import dd from './demo.json'
	import Test from './Test.vue';
	import {
		comp
	} from './test.js';
	import {
		comp as banana
	} from './test.js';
	import test from './testings.js';
	import {
		a,
		b,
		c,
		d,
		e,
		f
	} from './testings.js';
	test();
	console.log('dd', dd);
	console.log('comp', comp);
	console.log('banana', banana);
	const hey = 'Hallo på do';

</script>