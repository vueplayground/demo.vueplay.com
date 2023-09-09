<template>
	<TopMenu></TopMenu><router-view />
</template>
<script>
	import TopMenu from '@/vueplay/TopMenu.vue';
	export default {
		components: {
			TopMenu: TopMenu
		},
		data: () => ({})
	};

</script>
<style></style>