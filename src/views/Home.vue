<template>
	<div class="bg-slate-50 flex flex-col h-screen overflow-auto">
		<header class="">
			<div
				style="background-size:contain;background-position:center;background-repeat:no-repeat;width:266px;height:125px;margin-right:auto;margin-left:auto;margin-top:40px;position:relative;max-width:calc(100% - 100px);margin-bottom:-20px;left:5px"
				class="rounded-full logo"
			>
			</div>
			<h1
				style="width:calc(100% - 40px);margin:auto;margin-top:40px;margin-bottom:40px"
				class="text-center text-xl"
			>
				Lorem ipsum dolor sit amet
			</h1>
		</header>
		<main
			style="width:100%"
			class="grow"
		>
			<section
				style="width:100%"
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
			<section>
				<div
					style="background-size:contain;background-position:center;background-repeat:no-repeat;margin-right:auto;margin-left:auto;margin-top:70px;position:relative;margin-bottom:50px;max-width:calc(100% - 40px);aspect-ratio:1/.668;box-sizing:border-box;width:700px"
					class="rounded-3xl shadow-slate-200 shadow-xl screenshot"
				>
				</div>
			</section>
		</main>
	</div>
</template>
<script>
	export default {
		components: {},
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