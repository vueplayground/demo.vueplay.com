<template>
	<div
		:class="{'vp-float': float, 'vp-mobile': mobile, 'vp-open': open, 'dark': darkmode, 'z-10': !open, 'z-30': open}"
		:style="{'justify-content': align === 'right' ? 'flex-end' : 'flex-start'}"
		class="vp-rightmenu relative"
	>

		<div class="vp-mobile-icon">
			<button
				class="px-4"
				@click="open = !open"
			>
				<svg
					v-if="float"
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor"
					class="w-6 h-6"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						d="M12 6.75a.75.75 0 110-1.5.75.75 0 010 1.5zM12 12.75a.75.75 0 110-1.5.75.75 0 010 1.5zM12 18.75a.75.75 0 110-1.5.75.75 0 010 1.5z"
					/>
				</svg>

				<svg
					v-else
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor"
					class="w-6 h-6"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						d="M3.75 9h16.5m-16.5 6.75h16.5"
					/>
				</svg>
			</button>
		</div>

		<menu @click="open=false">
			<slot>
				<li :active="true">
					<router-link to="/">
						Home
					</router-link>
				</li>
				<li>
					<span @click="alert('About')">
						About
					</span>
				</li>
				<li>
					<router-link to="/more">
						More
					</router-link>
					<ul>
						<li>
							<router-link to="/blog">
								Blog
							</router-link>
						</li>
						<li>
							<span>Docs</span>
							<ul>
								<li>
									<span>Introduction</span>
								</li>
								<li>
									<span>How it works</span>
								</li>
							</ul>
						</li>
						<li>
							Discussion
						</li>
					</ul>
				</li>
				<li>
					<span>Contact</span>
				</li>
			</slot>
		</menu>

	</div>
</template>

<script>
	export default {
		emits: ['darkmode'],
		props: {
			breakpoint: {
				type: Number,
				default: 700
			},
			dark: {
				type: Boolean,
				default: false
			},
			color: {
				type: String,
				default: 'rgba(14, 58, 62, 1)'
			},
			background: {
				type: String,
				default: 'rgba(240,240,240,1)'
			},
			hover: {
				type: String,
				default: 'rgba(220,220,220,1)'
			},
			border: {
				type: String,
				default: 'rgba(251,178,60,1)'
			},
			colorDark: {
				type: String,
				default: 'rgba(240,240,240,1)'
			},
			backgroundDark: {
				type: String,
				default: 'rgba(75,75,75,1)'
			},
			hoverDark: {
				type: String,
				default: 'rgba(50,50,50,1)'
			},
			borderDark: {
				type: String,
				default: 'rgba(130,130,130,1)'
			},
			align: {
				type: String,
				default: 'left'
			},
			float: {
				type: Boolean,
				default: false
			}
		},
		data: () => ({
			open: false,
			mobile: false,
			forceDark: false
		}),
		computed: {
			darkmode() {
				return this.dark || this.forceDark
			}
		},
		watch: {
			open(isOpen) {
				if (isOpen) {
					document.body.classList.add('vp-hide-scroll')
				} else {
					document.body.classList.remove('vp-hide-scroll')
				}
			},
			forceDark(darkmode) {
				this.$emit('darkmode', darkmode)
			}
		},
		created() {
			this.onResize()
			window.addEventListener('resize', this.onResize)
		},
		beforeDestroy() {
			window.removeEventListener('resize', this.onResize)
		},
		methods: {
			onResize() {
				this.mobile = window.innerWidth < this.breakpoint
			}
		}
	};

</script>

<style>
	.vp-hide-scroll {
		overflow: hidden;
	}

	.vp-rightmenu {
		--bg-color: v-bind(background);
		--button-bg-color: var(--bg-color);
		--button-bg-hover-color: v-bind(hover);
		--button-text-color: v-bind(color);
		--border-color: v-bind(border);
		--dark-bg-color: v-bind(backgroundDark);
		--dark-button-bg-color: var(--dark-bg-color);
		--dark-button-bg-hover-color: v-bind(hoverDark);
		--dark-button-text-color: v-bind(colorDark);
		--dark-border-color: v-bind(borderDark);
		display: flex;
		transform: translateZ(0);
		width: 220px;
		max-width: 220px;
		min-width: 220px;
		background-color: var(--bg-color);
	}

	.vp-rightmenu.dark {
		background-color: var(--dark-bg-color);
	}

	.vp-rightmenu.vp-mobile {
		height: 40px;
		width: 100%;
		max-width: 100%;
		min-width: 0px;
	}

	.vp-rightmenu.vp-float.vp-mobile:not(.vp-open) {
		position: absolute;
		width: 50px;
		max-width: 50px;
		right: 0px;
		background-color: transparent;
	}
	.vp-rightmenu.vp-mobile:not(.vp-open) .vp-mobile-icon {
		background-color: transparent;
	}

	.vp-rightmenu.vp-mobile.vp-open {
		position: fixed !important;
		top: 0px;
		left: 0px;
		width: 100%;
	}

	.vp-rightmenu menu {
		display: inline-flex;
		flex-grow: 1;
		justify-content: flex-end;
	}

	.vp-rightmenu menu>li[active=true] {
		border-bottom: 3px solid var(--border-color);
		padding-top: 12px;
	}

	.vp-rightmenu.dark menu>li[active=true] {
		border-bottom: 3px solid var(--dark-border-color);
	}

	.vp-rightmenu menu li[active=true] {
		font-weight: 600;
	}

	.vp-rightmenu menu li[active=true] ul {
		font-weight: normal;
	}

	.vp-rightmenu li {
		position: relative;
		padding: 10px 10px;
		margin: 0px;
		display: inline-block;
		color: var(--button-text-color);
		cursor: pointer;
	}

	.vp-rightmenu ul li {
		background-color: var(--button-bg-color);
	}

	.vp-rightmenu.vp-mobile li {
		background-color: var(--button-bg-color);
	}

	.vp-rightmenu.dark li {
		color: var(--dark-button-text-color);
	}

	.vp-rightmenu.dark ul li {
		background-color: var(--dark-button-bg-color);
	}

	.vp-rightmenu.dark.vp-mobile li {
		background-color: var(--dark-button-bg-color);
	}

	.vp-rightmenu li>*:not(ul) {
		display: inline-flex;
		align-items: center;
	}

	.vp-rightmenu li>*:not(ul)::before {
		content: '';
		position: absolute;
		top: 0px;
		left: 0px;
		right: 0px;
		bottom: 0px;
		cursor: pointer;
	}

	.vp-rightmenu li:hover {
		background-color: var(--button-bg-hover-color);
	}

	.vp-rightmenu.dark li:hover {
		background-color: var(--dark-button-bg-hover-color);
	}

	.vp-rightmenu ul {
		display: none;
		box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.2), 0 1px 2px -1px rgb(0 0 0 / 0.2);
		border-radius: 2px;
	}

	.vp-rightmenu ul li {
		display: block;
		white-space: nowrap;
	}

	.vp-rightmenu ul li:has(ul)::before {
		content: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+CiAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBkPSJNNy43MiAxMi41M2EuNzUuNzUgMCAwMTAtMS4wNmw3LjUtNy41YS43NS43NSAwIDExMS4wNiAxLjA2TDkuMzEgMTJsNi45NyA2Ljk3YS43NS43NSAwIDExLTEuMDYgMS4wNmwtNy41LTcuNXoiIGNsaXAtcnVsZT0iZXZlbm9kZCIgLz4KPC9zdmc+Cg==");
		display: inline-block;
		width: 11px;
		margin-right: 10px;
	}

	.vp-rightmenu.dark ul li:has(ul)::before {
		filter: invert(100%);
	}

	.vp-rightmenu ul li:first-child {
		border-top-left-radius: 4px;
		border-top-right-radius: 4px;
	}

	.vp-rightmenu ul li:last-child {
		border-bottom-left-radius: 4px;
		border-bottom-right-radius: 4px;
	}

	.vp-rightmenu li:hover>ul {
		position: absolute;
		display: inline-block;
	}

	.vp-rightmenu li ul li ul {
		top: 0px;
		right: 100%;
	}

	.vp-rightmenu .vp-mobile-icon {
		display: none;
	}

	.vp-rightmenu.vp-mobile .vp-mobile-icon {
		display: inline-flex;
		justify-content: flex-end;
		align-items: center;
		height: 100%;
		background-color: var(--button-bg-color);
		color: var(--button-text-color);
	}

	.vp-rightmenu.dark .vp-mobile-icon {
		background-color: var(--dark-button-bg-color);
		color: var(--dark-button-text-color);
	}

	.vp-rightmenu .vp-mobile-icon button {
		height: 100%;
	}

	.vp-rightmenu .vp-mobile-icon button:hover {
		background-color: var(--button-bg-hover-color);
	}

	.vp-rightmenu.dark .vp-mobile-icon button:hover {
		background-color: var(--dark-button-bg-hover-color);
	}

	.vp-rightmenu .vp-mobile-icon button svg {
		transition: transform .25s linear;
	}

	.vp-rightmenu.vp-open .vp-mobile-icon button svg {
		transform: rotate(180deg);
	}

	.vp-rightmenu li:has(ul:hover):hover {
		background-color: var(--button-bg-color);
	}

	.vp-rightmenu.dark li:has(ul:hover):hover {
		background-color: var(--dark-button-bg-color);
	}

	.vp-rightmenu li:hover>ul {
		position: initial;
		display: block;
	}

	.vp-rightmenu menu>li:hover>ul {
		top: auto;
		right: auto;
	}

	.vp-rightmenu menu {
		top: 100%;
		width: 100%;
		height: 100%;
		background-color: var(--bg-color);
		overflow: auto;
		display: block;
		transition: height .1s linear, opacity .2s linear;
	}

	.vp-rightmenu.vp-mobile menu {
		position: fixed;
		top: 100%;
		height: 0px;
		opacity: 0;
	}

	.vp-rightmenu.vp-mobile.vp-open menu {
		position: fixed;
		top: 100%;
		width: 100%;
		height: calc(100vh - 100%);
	}

	.vp-rightmenu.vp-mobile.vp-open menu {
		height: calc(100vh - 100%);
		opacity: 1;
		overflow: auto;
		background-color: var(--bg-color);
		transition: height .2s linear, opacity .3s linear;
	}

	.vp-rightmenu.dark.vp-mobile.vp-open menu {
		background-color: var(--dark-bg-color);
	}

	.vp-rightmenu.dark menu {
		background-color: var(--dark-bg-color);
	}

	.vp-rightmenu menu>li {
		height: auto;
	}

	.vp-rightmenu li {
		position: relative;
		display: block;
		width: 100%;
		margin: 0px;
		text-align: left;
		padding: 20px 0px 20px 20px;
	}

	.vp-rightmenu ul li {
		margin-left: -20px;
		width: calc(100% + 20px);
	}

	.vp-rightmenu li:has(ul) {
		padding-bottom: 0px;
		padding-right: 0px;
	}

	.vp-rightmenu ul {
		display: block;
		width: 100%;
		margin: 20px 0px 0px;
		padding: 0px;
		box-shadow: none;
	}

	.vp-rightmenu ul li:has(ul)::before {
		content: '';
		display: initial;
		width: auto;
		margin-right: 0px;
	}

	.vp-rightmenu ul li::before {
		content: '';
		padding-left: 30px;
	}

	.vp-rightmenu ul li ul li::before {
		content: '';
		padding-left: 60px;
	}

	.vp-rightmenu ul li ul li ul li::before {
		content: '';
		padding-left: 90px;
	}

	.vp-rightmenu ul li ul li ul li ul li::before {
		content: '';
		padding-left: 120px;
	}

	.vp-rightmenu ul li ul li ul li ul li ul li::before {
		content: '';
		padding-left: 150px;
	}

</style>