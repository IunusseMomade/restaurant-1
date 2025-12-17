<script>
	import { Menu, X } from '@lucide/svelte';
	import * as m from '$lib/paraglide/messages';
	import { localizeHref } from '$lib/paraglide/runtime';

	let isMenuOpen = $state(false);
</script>

<header class="flex w-full flex-col border-b border-gray-200 bg-white">
	<!-- Main Nav Bar -->
	<div class="container mx-auto flex items-center justify-between px-6 py-4">
		<!-- Brand Logo Placeholder -->
		<div class="flex items-center gap-2">
			<a href={localizeHref('/')} class="flex items-center gap-2 text-inherit no-underline">
				<div class="font-serif text-3xl font-bold tracking-wider">SHAMIANA</div>
				<div class="mx-2 h-8 w-[1px] bg-gray-300"></div>
				<div class="text-xs leading-tight uppercase tracking-[0.2em] text-gray-500">
					{@html m.brand_est()}
				</div>
			</a>
		</div>

		<!-- Desktop Nav Actions -->
		<div class="hidden items-center gap-8 text-sm font-medium tracking-wide md:flex">
			<a href={localizeHref('/locations')} class="link-hover">{m.nav_locations()}</a>
			<a href={localizeHref('/menu')} class="link-hover">{m.nav_menu()}</a>
			<a href={localizeHref('/about')} class="link-hover">{m.nav_story()}</a>
			<a href={localizeHref('/contact')} class="link-hover">{m.nav_contact()}</a>

			<div class="ml-4 flex items-center gap-4">
				<button
					class="btn-primary px-6 py-2.5 text-xs"
				>
					{m.nav_order()}
				</button>
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
		<div class="border-t border-gray-100 bg-white px-6 py-6 md:hidden">
			<nav class="flex flex-col gap-6 text-sm font-medium tracking-wide">
				<a href={localizeHref('/locations')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_locations()}</a>
				<a href={localizeHref('/menu')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_menu()}</a>
				<a href={localizeHref('/about')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_story()}</a>
				<a href={localizeHref('/contact')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_contact()}</a>
				<div class="h-[1px] w-full bg-gray-100"></div>
				<div class="flex flex-col gap-4">
					<button class="btn-primary w-full text-center"> {m.nav_order()} </button>
				</div>
			</nav>
		</div>
	{/if}
</header>
