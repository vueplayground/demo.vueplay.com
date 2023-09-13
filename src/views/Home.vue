<template>
	<div class="bg-slate-50 flex flex-col overflow-auto">
		<Carousel
			class="shadow-2xl shadow-slate-500 rounded-md md:mt-6 mx-auto"
			style="max-width:700px;overflow:hidden"
		><img
				src="@/assets/launch.png"
				width="100"
				height="100"
			/><img
				src="https://images.wallpaperscraft.com/image/single/pool_building_columns_990136_1600x900.jpg"
				width="100"
				height="100"
			/><img
				src="https://images.wallpaperscraft.com/image/single/starry_sky_night_tree_117028_1600x900.jpg"
				width="100"
				height="100"
			/></Carousel>
		<main
			style="width:100%;margin-top:85px"
			class="grow"
		>
			<section
				style="width:100%;padding-bottom:60px"
				class="text-center"
			>
				<button
					@click="$router.push('/')"
					class="duration-300 transition-shadow ease-linear rounded mr-3 p-3 bg-slate-200 hover:drop-shadow-lg drop-shadow"
				>
					Home
				</button> <button
					@click="$router.push('/about')"
					class="duration-300 transition-shadow ease-linear rounded mr-3 p-3 bg-slate-200 hover:drop-shadow-lg drop-shadow"
				>
					About
				</button><button
					@click="$router.push('/contact')"
					class="rounded p-3 bg-purple-400 from-purple-500 bg-gradient-to-br hover:bg-purple-600 hover:from-purple-600 text-white duration-300 transition hover:drop-shadow-lg drop-shadow"
				>
					Contact ⇾
				</button>
			</section>
		</main>
	</div>
</template>
<script>
	import Carousel from '@/vueplay/Carousel.vue';
	export default {
		components: {
			Carousel: Carousel
		},
		data: () => ({}),
		methods: {
			open(url) {
				location.href = url;
			}
		}
	};

</script>
<style scoped>
	.logo {
		background-image: url(@/assets/your-logo.png);
	}

	.screenshot {
		background-image: url(@/assets/launch.png);
	}

</style>