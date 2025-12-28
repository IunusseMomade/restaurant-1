<script>
	import { fade, slide } from 'svelte/transition';
	import { Menu, X } from '@lucide/svelte';
	import * as m from '$lib/paraglide/messages';
	import { localizeHref } from '$lib/paraglide/runtime';
	import logo from '$lib/assets/ir-logo.png';

	let isMenuOpen = $state(false);
</script>

<header class="relative z-40 flex w-full flex-col border-b border-gray-200 bg-white">
	<div class="container mx-auto flex items-center justify-between px-6 py-4">
		<!-- Brand -->
		<div class="flex items-center">
			<a
				href={localizeHref('/')}
				class="inline-flex items-center gap-3 text-inherit no-underline"
				aria-label="Restaurant Istanbul"
			>
				<img
					src={logo}
					alt="Restaurant Istanbul"
					class="h-10 w-auto object-contain"
				/>
				<span
					class="hidden sm:block font-serif text-2xl font-semibold tracking-[0.06em] leading-none "
				>
					ISTANBUL
				</span>
			</a>
		</div>

		<!-- Desktop Nav Actions -->
		<div class="hidden items-center gap-8 text-sm font-medium tracking-wide md:flex">
			<a href={localizeHref('/locations')} class="link-hover">{m.nav_locations()}</a>
			<a href={localizeHref('/menu')} class="link-hover">{m.nav_menu()}</a>
			<a href={localizeHref('/about')} class="link-hover">{m.nav_story()}</a>
			<a href={localizeHref('/contact')} class="link-hover">{m.nav_contact()}</a>

			<div class="ml-4 flex items-center gap-4">
				<a
					href="https://wa.me/258847131300"
					target="_blank"
					rel="noopener noreferrer"
					class="btn-primary px-6 py-2.5 text-xs inline-block"
				>
					{m.nav_order()}
				</a>
			</div>
		</div>

		<!-- Mobile Menu Toggle -->
		<button class="md:hidden" onclick={() => (isMenuOpen = !isMenuOpen)}>
			{#if isMenuOpen}
				<X size={24} />
			{:else}
				<Menu size={24} />
			{/if}
		</button>
	</div>

	<!-- Mobile Menu -->
	{#if isMenuOpen}
		<!-- backdrop -->
		<div
			class="fixed inset-0 z-20 bg-black/40 md:hidden"
			transition:fade={{ duration: 140 }}
			onclick={() => (isMenuOpen = false)}
		></div>

		<div
			class="relative z-30 border-t border-gray-100 bg-white px-6 py-6 md:hidden"
			transition:slide={{ duration: 180 }}
		>
			<nav class="flex flex-col gap-6 text-sm font-medium tracking-wide">
				<a href={localizeHref('/locations')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_locations()}</a>
				<a href={localizeHref('/menu')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_menu()}</a>
				<a href={localizeHref('/about')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_story()}</a>
				<a href={localizeHref('/contact')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_contact()}</a>
				<div class="h-[1px] w-full bg-gray-100"></div>
				<div class="flex flex-col gap-4">
					<a href="https://wa.me/258847131300" target="_blank" rel="noopener noreferrer" class="btn-primary w-full text-center"> {m.nav_order()} </a>
				</div>
			</nav>
		</div>
	{/if}
</header>
