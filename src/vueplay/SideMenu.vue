<template>
	<div
		:class="{'vp-mobile': mobile, 'vp-open': open, 'dark': darkmode}"
		class="vp-leftmenu relative z-20"
	>

		<div class="vp-mobile-icon">
			<button
				class="px-4"
				@click="open = !open"
			>
				<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
					<path stroke-linecap="round" stroke-linejoin="round" d="M3.75 9h16.5m-16.5 6.75h16.5" />
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
				default: 640
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

	.vp-leftmenu {
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
		width: 250px;
		max-width: 250px;
		background-color: var(--bg-color);
	}

	.vp-leftmenu.dark {
		background-color: var(--dark-bg-color);
	}

	.vp-leftmenu.vp-mobile {
		height: 40px;
		width: 100%;
		max-width: 100%;
	}

	.vp-leftmenu.vp-mobile.vp-open {
		position: fixed;
		top: 0px;
		left: 0px;
		width: 100%;
	}

	.vp-leftmenu menu {
		display: inline-flex;
		flex-grow: 1;
		justify-content: flex-end;
	}

	.vp-leftmenu menu>li[active=true] {
		border-bottom: 3px solid var(--border-color);
		padding-top: 12px;
	}

	.vp-leftmenu.dark menu>li[active=true] {
		border-bottom: 3px solid var(--dark-border-color);
	}

	.vp-leftmenu menu li[active=true] {
		font-weight: 600;
	}

	.vp-leftmenu menu li[active=true] ul {
		font-weight: normal;
	}

	.vp-leftmenu li {
		position: relative;
		padding: 10px 10px;
		margin: 0px;
		display: inline-block;
		color: var(--button-text-color);
		cursor: pointer;
	}

	.vp-leftmenu ul li {
		background-color: var(--button-bg-color);
	}

	.vp-leftmenu.vp-mobile li {
		background-color: var(--button-bg-color);
	}

	.vp-leftmenu.dark li {
		color: var(--dark-button-text-color);
	}

	.vp-leftmenu.dark ul li {
		background-color: var(--dark-button-bg-color);
	}

	.vp-leftmenu.dark.vp-mobile li {
		background-color: var(--dark-button-bg-color);
	}

	.vp-leftmenu li>*:not(ul) {
		display: inline-flex;
		align-items: center;
	}

	.vp-leftmenu li>*:not(ul)::before {
		content: '';
		position: absolute;
		top: 0px;
		left: 0px;
		right: 0px;
		bottom: 0px;
		cursor: pointer;
	}

	.vp-leftmenu li:hover {
		background-color: var(--button-bg-hover-color);
	}

	.vp-leftmenu.dark li:hover {
		background-color: var(--dark-button-bg-hover-color);
	}

	.vp-leftmenu ul {
		display: none;
		box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.2), 0 1px 2px -1px rgb(0 0 0 / 0.2);
		border-radius: 2px;
	}

	.vp-leftmenu ul li {
		display: block;
		white-space: nowrap;
	}

	.vp-leftmenu ul li:has(ul)::before {
		content: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+CiAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBkPSJNNy43MiAxMi41M2EuNzUuNzUgMCAwMTAtMS4wNmw3LjUtNy41YS43NS43NSAwIDExMS4wNiAxLjA2TDkuMzEgMTJsNi45NyA2Ljk3YS43NS43NSAwIDExLTEuMDYgMS4wNmwtNy41LTcuNXoiIGNsaXAtcnVsZT0iZXZlbm9kZCIgLz4KPC9zdmc+Cg==");
		display: inline-block;
		width: 11px;
		margin-right: 10px;
	}

	.vp-leftmenu.dark ul li:has(ul)::before {
		filter: invert(100%);
	}

	.vp-leftmenu ul li:first-child {
		border-top-left-radius: 4px;
		border-top-right-radius: 4px;
	}

	.vp-leftmenu ul li:last-child {
		border-bottom-left-radius: 4px;
		border-bottom-right-radius: 4px;
	}

	.vp-leftmenu li:hover>ul {
		position: absolute;
		display: inline-block;
	}

	.vp-leftmenu li ul li ul {
		top: 0px;
		right: 100%;
	}

	.vp-leftmenu .vp-mobile-icon {
		display: none;
	}

	.vp-leftmenu.vp-mobile .vp-mobile-icon {
		display: inline-flex;
		justify-content: flex-end;
		align-items: center;
		height: 100%;
		background-color: var(--button-bg-color);
		color: var(--button-text-color);
	}

	.vp-leftmenu.dark .vp-mobile-icon {
		background-color: var(--dark-button-bg-color);
		color: var(--dark-button-text-color);
	}

	.vp-leftmenu .vp-mobile-icon button {
		height: 100%;
	}

	.vp-leftmenu .vp-mobile-icon button:hover {
		background-color: var(--button-bg-hover-color);
	}

	.vp-leftmenu.dark .vp-mobile-icon button:hover {
		background-color: var(--dark-button-bg-hover-color);
	}

	.vp-leftmenu .vp-mobile-icon button svg {
		transition: transform .25s linear;
	}

	.vp-leftmenu.vp-open .vp-mobile-icon button svg {
		transform: rotate(180deg);
	}

	.vp-leftmenu li:has(ul:hover):hover {
		background-color: var(--button-bg-color);
	}

	.vp-leftmenu.dark li:has(ul:hover):hover {
		background-color: var(--dark-button-bg-color);
	}

	.vp-leftmenu li:hover>ul {
		position: initial;
		display: block;
	}

	.vp-leftmenu menu>li:hover>ul {
		top: auto;
		right: auto;
	}

	.vp-leftmenu menu {
		top: 100%;
		width: 100%;
		height: 100%;
		background-color: var(--bg-color);
		overflow: auto;
		display: block;
		transition: height .1s linear, opacity .2s linear;
	}

	.vp-leftmenu.vp-mobile menu {
		position: fixed;
		top: 100%;
		height: 0px;
		opacity: 0;
	}

	.vp-leftmenu.vp-mobile.vp-open menu {
		position: fixed;
		top: 100%;
		width: 100%;
		height: calc(100vh - 100%);
	}

	.vp-leftmenu.vp-mobile.vp-open menu {
		height: calc(100vh - 100%);
		opacity: 1;
		overflow: auto;
		background-color: var(--bg-color);
		transition: height .2s linear, opacity .3s linear;
	}

	.vp-leftmenu.dark.vp-mobile.vp-open menu {
		background-color: var(--dark-bg-color);
	}

	.vp-leftmenu.dark menu {
		background-color: var(--dark-bg-color);
	}

	.vp-leftmenu menu>li {
		height: auto;
	}

	.vp-leftmenu li {
		position: relative;
		display: block;
		width: 100%;
		margin: 0px;
		text-align: left;
		padding: 20px 0px 20px 20px;
	}

	.vp-leftmenu ul li {
		margin-left: -20px;
		width: calc(100% + 20px);
	}

	.vp-leftmenu li:has(ul) {
		padding-bottom: 0px;
		padding-right: 0px;
	}

	.vp-leftmenu ul {
		display: block;
		width: 100%;
		margin: 20px 0px 0px;
		padding: 0px;
		box-shadow: none;
	}

	.vp-leftmenu ul li:has(ul)::before {
		content: '';
		display: initial;
		width: auto;
		margin-right: 0px;
	}

	.vp-leftmenu ul li::before {
		content: '';
		padding-left: 30px;
	}

	.vp-leftmenu ul li ul li::before {
		content: '';
		padding-left: 60px;
	}

	.vp-leftmenu ul li ul li ul li::before {
		content: '';
		padding-left: 90px;
	}

	.vp-leftmenu ul li ul li ul li ul li::before {
		content: '';
		padding-left: 120px;
	}

	.vp-leftmenu ul li ul li ul li ul li ul li::before {
		content: '';
		padding-left: 150px;
	}

</style>