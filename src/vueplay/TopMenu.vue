<template>
	<div
		:class="{'vp-mobile': mobile, 'vp-open': open, 'dark': darkmode}"
		class="vp-topmenu relative z-20"
	>

		<div class="vp-logo">
			<slot name="logo">
				<router-view to="/" style="display: inline-flex">
					<svg
						xmlns="http://www.w3.org/2000/svg"
						viewBox="0 0 24 24"
						class="ml-4 w-12 vp-demo-icon"
					>
						<path fill-rule="evenodd"
							d="M12.963 2.286a.75.75 0 00-1.071-.136 9.742 9.742 0 00-3.539 6.177A7.547 7.547 0 016.648 6.61a.75.75 0 00-1.152-.082A9 9 0 1015.68 4.534a7.46 7.46 0 01-2.717-2.248zM15.75 14.25a3.75 3.75 0 11-7.313-1.172c.628.465 1.35.81 2.133 1a5.99 5.99 0 011.925-3.545 3.75 3.75 0 013.255 3.717z"
							clip-rule="evenodd" />
					</svg>
					<div class="text-2xl ml-3" style="display: inline-flex; align-items: center">
						logo
					</div>
				</router-view>
			</slot>
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
								<li>
									<span>FAQ</span>
									<ul>
										<li>
											<span>How?</span>
										</li>
										<li>
											Why?
										</li>
										<li>
											<span>When?</span>
										</li>
									</ul>
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

		<div class="vp-end-menu">
			<div class="vp-divider"/>
			<slot name="end-before"></slot>
			<slot name="end">
				<div @click="forceDark = !forceDark">
					<svg
						v-if="darkmode"
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="currentColor"
						class="w-5 h-5 vp-moon"
					>
						<path stroke-linecap="round" stroke-linejoin="round" d="M21.752 15.002A9.718 9.718 0 0118 15.75c-5.385 0-9.75-4.365-9.75-9.75 0-1.33.266-2.597.748-3.752A9.753 9.753 0 003 11.25C3 16.635 7.365 21 12.75 21a9.753 9.753 0 009.002-5.998z" />
					</svg>
					<svg
						v-else
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="currentColor"
						class="w-5 h-5 vp-sun"
					>
						<path stroke-linecap="round" stroke-linejoin="round" d="M12 3v2.25m6.364.386l-1.591 1.591M21 12h-2.25m-.386 6.364l-1.591-1.591M12 18.75V21m-4.773-4.227l-1.591 1.591M5.25 12H3m4.227-4.773L5.636 5.636M15.75 12a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0z" />
					</svg>
				</div>
			</slot>
			<slot name="end-after"></slot>
		</div>

		<div class="vp-mobile-icon" >
			<button class="px-6" @click="open = !open">
				<svg  xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"
					class="w-8">
					<path fill-rule="evenodd"
						d="M3 6.75A.75.75 0 013.75 6h16.5a.75.75 0 010 1.5H3.75A.75.75 0 013 6.75zM3 12a.75.75 0 01.75-.75h16.5a.75.75 0 010 1.5H3.75A.75.75 0 013 12zm0 5.25a.75.75 0 01.75-.75h16.5a.75.75 0 010 1.5H3.75a.75.75 0 01-.75-.75z"
						clip-rule="evenodd" />
				</svg>
			</button>
		</div>
	</div>
</template>

<script>
export default {
	emits: ['darkmode'],
	props: {
		breakpoint: {
			type: Number,
			default: 568
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

<style scoped>
/**
	TODO: Allow slotted selectors when scoped
	Then the .topmenu class can be skipped
**/
:slotted(li) {
	color: red;
	/* Should apply to the slotted scope */
}

:deep(li) {
	color: green;
	/* Should affect child components */
}

:global(li) {
	color: blue;
	/* Should apply to the global scope */
}
</style>

<style>

.vp-hide-scroll {
	overflow: hidden;
}

.vp-topmenu {
	/*
	--bg-color: rgba(240,240,240,1);
	--button-bg-color: var(--bg-color);
	--button-bg-hover-color: rgba(220,220,220,1);
	--button-text-color: rgba(14, 58, 62, 1);
	--border-color: rgba(251,178,60,1);

	--dark-bg-color: rgba(75,75,75,1);
	--dark-button-bg-color: var(--dark-bg-color);
	--dark-button-bg-hover-color: rgba(50,50,50,1);
	--dark-button-text-color: rgba(240,240,240,1);
	--dark-border-color: rgba(130,130,130,1);
	*/
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
	width: 100%;
	height: 80px;
	background-color: var(--bg-color);
}

.vp-topmenu.dark {
	background-color: var(--dark-bg-color);
}

.vp-topmenu.vp-mobile.vp-open {
	position: fixed;
	top: 0px;
	left: 0px;
	width: 100%;
}

.vp-topmenu .vp-logo {
	display: inline-flex;
	height: 100%;
	color: var(--button-text-color);
}

.vp-topmenu.dark .vp-logo {
	display: inline-flex;
	height: 100%;
	color: var(--dark-button-text-color);
}

.vp-topmenu .vp-demo-icon {
	fill: var(--border-color);
}

.vp-topmenu.dark .vp-demo-icon {
	fill: var(--dark-border-color);
}

.vp-topmenu .vp-moon {
	fill: var(--button-text-color);
	stroke: var(--button-text-color);
}

.vp-topmenu.dark .vp-moon {
	fill: var(--dark-button-text-color);
	stroke: var(--dark-button-text-color);
}

.vp-topmenu .vp-sun {
	stroke: var(--button-text-color);
}

.vp-topmenu.dark .vp-sun {
	stroke: var(--dark-button-text-color);
}

.vp-topmenu .vp-logo>* {
	display: inline-flex;
	height: 100%;
	align-items: center;
	cursor: pointer;
}

.vp-topmenu menu {
	display: inline-flex;
	flex-grow: 1;
	justify-content: flex-end;
}

.vp-topmenu menu>li {
	height: 100%;
	display: inline-flex;
	margin: 0px;
	align-items: center;
	transition: all .2s linear;
}

.vp-topmenu menu>li:last-child {
	padding-right: 20px;
}

.vp-topmenu menu>li:first-child {
	padding-right: 10px;
}

.vp-topmenu:not(.vp-mobile) menu>li:has(ul) {
	padding-right: 35px;
}

.vp-topmenu:not(.vp-mobile) menu>li:has(ul):last-child {
	padding-right: 10px;
}

.vp-topmenu:not(.vp-mobile) menu>li:has(ul)::after {
	position: absolute;
	top: calc(50% + 1px);
	right: 10px;
	transform: translateY(-50%);
	content: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGZpbGw9Im5vbmUiIHZpZXdCb3g9IjAgMCAyNCAyNCIgc3Ryb2tlLXdpZHRoPSIxLjUiIHN0cm9rZT0iY3VycmVudENvbG9yIiBjbGFzcz0idy01IGgtNSI+CiAgPHBhdGggc3Ryb2tlLWxpbmVjYXA9InJvdW5kIiBzdHJva2UtbGluZWpvaW49InJvdW5kIiBkPSJNMTkuNSA4LjI1bC03LjUgNy41LTcuNS03LjUiIC8+Cjwvc3ZnPgo=");
	width: 15px;
	margin-left: 10px;
}

.vp-topmenu.dark:not(.vp-mobile) menu>li:has(ul)::after {
	filter: invert(100%);
}

.vp-topmenu menu>li[active=true] {
	border-bottom: 3px solid var(--border-color);
	padding-top: 12px;
}

.vp-topmenu.dark menu>li[active=true] {
	border-bottom: 3px solid var(--dark-border-color);
}

.vp-topmenu menu li[active=true] {
	font-weight: 600;
}

.vp-topmenu menu li[active=true] ul {
	font-weight: normal;
}

.vp-topmenu menu>li:hover>ul {
	top: 100%;
	right: 0px;
}

.vp-topmenu li {
	position: relative;
	padding: 10px 10px;
	margin: 0px;
	display: inline-block;
	color: var(--button-text-color);
	cursor: pointer;
}

.vp-topmenu.vp-mobile li {
	background-color: var(--button-bg-color);
}

.vp-topmenu.dark li {
	color: var(--dark-button-text-color);
}

.vp-topmenu.dark.vp-mobile li {
	background-color: var(--dark-button-bg-color);
}

.vp-topmenu li > *:not(ul) {
	display: inline-flex;
	align-items: center;
}

.vp-topmenu li > *:not(ul)::before {
	content: '';
	position: absolute;
	top: 0px;
	left: 0px;
	right: 0px;
	bottom: 0px;
	cursor: pointer;
}

.vp-topmenu li:hover {
	background-color: var(--button-bg-hover-color);
}

.vp-topmenu.dark li:hover {
	background-color: var(--dark-button-bg-hover-color);
}

.vp-topmenu ul {
	display: none;
	box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.2), 0 1px 2px -1px rgb(0 0 0 / 0.2);
	border-radius: 2px;
}

.vp-topmenu ul li {
	display: block;
	text-align: right;
	white-space: nowrap;
}

.vp-topmenu ul li:has(ul)::before {
	content: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+CiAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBkPSJNNy43MiAxMi41M2EuNzUuNzUgMCAwMTAtMS4wNmw3LjUtNy41YS43NS43NSAwIDExMS4wNiAxLjA2TDkuMzEgMTJsNi45NyA2Ljk3YS43NS43NSAwIDExLTEuMDYgMS4wNmwtNy41LTcuNXoiIGNsaXAtcnVsZT0iZXZlbm9kZCIgLz4KPC9zdmc+Cg==");
	display: inline-block;
	width: 11px;
	margin-right: 10px;
}

.vp-topmenu.dark ul li:has(ul)::before {
	filter: invert(100%);
}

.vp-topmenu ul li:first-child {
	border-top-left-radius: 4px;
	border-top-right-radius: 4px;
}

.vp-topmenu ul li:last-child {
	border-bottom-left-radius: 4px;
	border-bottom-right-radius: 4px;
}

.vp-topmenu li:hover>ul {
	position: absolute;
	display: inline-block;
}

.vp-topmenu li ul li ul {
	top: 0px;
	right: 100%;
}

.vp-topmenu li ul li ul li {
	text-align: right;
}

.vp-topmenu .vp-end-menu {
	display: flex;
}

.vp-topmenu .vp-end-menu > * {
	display: inline-flex;
	align-items: center;
	height: 100%;
	box-sizing: content-box;
}

.vp-topmenu .vp-end-menu > *:not(.vp-divider) {
	padding: 0px 5px;
	cursor: pointer;
}

.vp-topmenu .vp-end-menu > *:not(.vp-divider):nth-child(2) {
	padding-left: 15px;
}

.vp-topmenu .vp-end-menu > *:not(.vp-divider):last-child {
	padding-right: 15px;
}

.vp-topmenu .vp-end-menu > *:not(.vp-divider):hover {
	background-color: var(--button-bg-hover-color);
}

.vp-topmenu.dark .vp-end-menu > *:not(.vp-divider):hover {
	background-color: var(--dark-button-bg-hover-color);
}

.vp-topmenu .vp-end-menu .vp-divider {
	position: relative;
	top: 35%;
	height: 30%;
	width: 1px;
	background-color: var(--button-text-color);
}

.vp-topmenu.dark .vp-end-menu .vp-divider {
	position: relative;
	top: 35%;
	height: 30%;
	width: 1px;
	background-color: var(--dark-button-text-color);
}

.vp-topmenu .vp-mobile-icon {
	display: none;
}

.vp-topmenu .vp-end-menu > .vp-divider:only-child,
.vp-topmenu.vp-mobile .vp-end-menu .vp-divider {
	display: none;
}

.vp-topmenu.vp-mobile .vp-end-menu {
	flex-grow: 1;
	justify-content: flex-end;
}

.vp-topmenu.vp-mobile .vp-mobile-icon {
	display: inline-flex;
    justify-content: flex-end;
	align-items: center;
	height: 100%;
	color: var(--button-text-color);
}

.vp-topmenu.dark.vp-mobile .vp-mobile-icon {
	color: var(--dark-button-text-color);
}

.vp-topmenu.vp-mobile .vp-mobile-icon button {
	height: 100%;
}

.vp-topmenu.vp-mobile .vp-mobile-icon button:hover {
	background-color: var(--button-bg-hover-color);
}

.vp-topmenu.dark.vp-mobile .vp-mobile-icon button:hover {
	background-color: var(--dark-button-bg-hover-color);
}

.vp-topmenu.vp-mobile .vp-mobile-icon button svg {
	transition: transform .25s linear;
}

.vp-topmenu.vp-mobile.vp-open .vp-mobile-icon button svg {
	transform: rotate(180deg);
}

.vp-topmenu.vp-mobile li:has(ul:hover):hover {
	background-color: var(--button-bg-color);
}

.vp-topmenu.dark.vp-mobile li:has(ul:hover):hover {
	background-color: var(--dark-button-bg-color);
}

.vp-topmenu.vp-mobile li:hover>ul {
	position: initial;
	display: block;
}

.vp-topmenu.vp-mobile menu>li:hover>ul {
	top: auto;
	right: auto;
}

.vp-topmenu.vp-mobile menu {
	position: fixed;
	top: 100%;
	width: 100%;
	height: 0px;
	opacity: 0;
	overflow: hidden;
	display: block;
	transition: height .1s linear, opacity .2s linear;
}

.vp-topmenu.vp-mobile.vp-open menu {
	height: calc(100vh - 100%);
	opacity: 1;
	overflow: auto;
	background-color: var(--bg-color);
	transition: height .2s linear, opacity .3s linear;
}

.vp-topmenu.dark.vp-mobile.vp-open menu {
	background-color: var(--dark-bg-color);
}

.vp-topmenu.vp-mobile menu>li {
	height: auto;
}

.vp-topmenu.vp-mobile li {
	position: relative;
	display: block;
	width: 100%;
	margin: 0px;
	text-align: left;
	padding: 20px 0px 20px 20px;
}

.vp-topmenu.vp-mobile ul li {
	margin-left: -20px;
	width: calc(100% + 20px);
}

.vp-topmenu.vp-mobile li:has(ul) {
	padding-bottom: 0px;
	padding-right: 0px;
}

.vp-topmenu.vp-mobile ul {
	display: block;
	width: 100%;
	margin: 20px 0px 0px;
	padding: 0px;
	box-shadow: none;
}

.vp-topmenu.vp-mobile ul li:has(ul)::before {
	content: '';
	display: initial;
	width: auto;
	margin-right: 0px;
}

.vp-topmenu.vp-mobile ul li::before {
	content: '';
	padding-left: 30px;
}

.vp-topmenu.vp-mobile ul li ul li::before {
	content: '';
	padding-left: 60px;
}

.vp-topmenu.vp-mobile ul li ul li ul li::before {
	content: '';
	padding-left: 90px;
}

.vp-topmenu.vp-mobile ul li ul li ul li ul li::before {
	content: '';
	padding-left: 120px;
}

.vp-topmenu.vp-mobile ul li ul li ul li ul li ul li::before {
	content: '';
	padding-left: 150px;
}

</style>