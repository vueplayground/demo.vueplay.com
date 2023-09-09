<template>
	<div
		:class="{'vp-mobile': mobile, 'vp-open': open}"
		class="vp-topmenu relative"
	>

		<div class="vp-logo">
			<slot name="logo">
				<a href="#" style="display: inline-flex">
					<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="orange" class="ml-4 w-12">
						<path fill-rule="evenodd"
							d="M12.963 2.286a.75.75 0 00-1.071-.136 9.742 9.742 0 00-3.539 6.177A7.547 7.547 0 016.648 6.61a.75.75 0 00-1.152-.082A9 9 0 1015.68 4.534a7.46 7.46 0 01-2.717-2.248zM15.75 14.25a3.75 3.75 0 11-7.313-1.172c.628.465 1.35.81 2.133 1a5.99 5.99 0 011.925-3.545 3.75 3.75 0 013.255 3.717z"
							clip-rule="evenodd" />
					</svg>
					<div class="text-2xl ml-3" style="display: inline-flex; align-items: center">
						logo
					</div>
				</a>
			</slot>
		</div>

		<menu>
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
	props: {
		breakpoint: {
			type: Number,
			default: 568
		}
	},
	data: () => ({
		open: false,
		mobile: false
	}),
	created() {
		this.onResize()
		window.addEventListener('resize', this.onResize)
	},
	beforeDestroy() {
		window.removeEventListener('resize', this.onResize)
	},
	methods: {
		onResize() {
			this.mobile = window.innerWidth < this
				.breakpoint
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
.vp-topmenu {
	--bg-color: rgba(192, 216, 210, 1);
	--button-bg-color: var(--bg-color);
	--button-bg-hover-color: rgba(174, 195, 190, 1);
	--button-text-color: rgba(14, 58, 62, 1);

	position: absolute;
	display: flex;
	width: 100%;
	height: 80px;
	background-color: var(--bg-color);
}

.vp-topmenu .vp-logo {
	display: inline-flex;
	height: 100%;
}

.vp-topmenu .vp-logo>* {
	display: inline-flex;
	height: 100%;
	align-items: center;
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
	padding-right: 5px;
}

.vp-topmenu:not(.vp-mobile) menu>li:has(ul):last-child {
	padding-right: 10px;
}

.vp-topmenu:not(.vp-mobile) menu>li:has(ul)::after {
	content: url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+CiAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBkPSJNMTIuNTMgMTYuMjhhLjc1Ljc1IDAgMDEtMS4wNiAwbC03LjUtNy41YS43NS43NSAwIDAxMS4wNi0xLjA2TDEyIDE0LjY5bDYuOTctNi45N2EuNzUuNzUgMCAxMTEuMDYgMS4wNmwtNy41IDcuNXoiIGNsaXAtcnVsZT0iZXZlbm9kZCIgLz4KPC9zdmc+Cg==");
	width: 15px;
	margin-left: 10px;
}

.vp-topmenu menu>li[active=true] {
	border-bottom: 3px solid rgba(246, 171, 49, 1);
	padding-top: 12px;
	font-weight: 600;
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
	background-color: var(--button-bg-color);
	color: var(--button-text-color);
	cursor: pointer;
}

.vp-topmenu li > *:not(ul) {
	display: inline-flex;
	align-items: center;
}

.vp-topmenu li > *:not(ul)::after {
	content: '';
	position: absolute;
	top: 0px;
	left: 0px;
	right: 0px;
	bottom: 0px;
}

.vp-topmenu li:hover {
	background-color: var(--button-bg-hover-color);
}

.vp-topmenu ul {
	display: none;
	box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.2), 0 1px 2px -1px rgb(0 0 0 / 0.2);
	border-radius: 4px;
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

.vp-topmenu .vp-mobile-icon {
	display: none;
}

.vp-topmenu.vp-mobile .vp-mobile-icon {
	display: inline-flex;
	flex-grow: 1;
    justify-content: flex-end;
	align-items: center;
	height: 100%;
}

.vp-topmenu.vp-mobile .vp-mobile-icon button {
	height: 100%;
}

.vp-topmenu.vp-mobile .vp-mobile-icon button:hover {
	background-color: var(--button-bg-hover-color);
}

.vp-topmenu.vp-mobile li:has(ul:hover):hover {
	background-color: var(--button-bg-color);
}

.vp-topmenu.vp-mobile menu {
	display: none;
}

.vp-topmenu.vp-mobile li:hover>ul {
	position: initial;
	display: block;
}

.vp-topmenu.vp-mobile menu>li:hover>ul {
	top: auto;
	right: auto;
}

.vp-topmenu.vp-mobile.vp-open menu {
	position: absolute;
	top: 100%;
	display: block;
	width: 100%;
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
	display: inline-block;
	width: auto;
	margin-right: -4px;
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

</style>