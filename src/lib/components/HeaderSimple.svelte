<script>
	import { onMount } from 'svelte';
	import { fade, slide } from 'svelte/transition';
	import { Menu, X } from '@lucide/svelte';
	import * as m from '$lib/paraglide/messages';
	import { localizeHref } from '$lib/paraglide/runtime';
	import logo from '$lib/assets/ir-logo.png?enhanced';

	let { forceSolid = false } = $props();

	let isMenuOpen = $state(false);
	let isScrolled = $state(false);

	const navSolid = $derived(forceSolid || isScrolled || isMenuOpen);
	const navLinkClass = $derived(navSolid ? 'link-hover' : 'link-hover text-white/90 hover:text-white');

	onMount(() => {
		const onScroll = () => {
			isScrolled = window.scrollY > 8;
		};

		onScroll();
		window.addEventListener('scroll', onScroll, { passive: true });

		return () => window.removeEventListener('scroll', onScroll);
	});

	$effect(() => {
		// prevent background scroll when mobile menu is open
		if (typeof document !== 'undefined') document.body.style.overflow = isMenuOpen ? 'hidden' : '';
		return () => {
			if (typeof document !== 'undefined') document.body.style.overflow = '';
		};
	});
</script>

<header class="relative flex w-full flex-col">
	<!-- Top Nav overlaying hero (matches Header.svelte behavior) -->
	<div class="absolute inset-x-0 top-0 z-30">
		<div
			class={`relative z-40 ${
				navSolid
					? 'bg-white/95 text-gray-900 backdrop-blur border-b border-gray-200'
					: 'bg-transparent text-white border-b border-transparent'
			}`}
		>
			<div class="container mx-auto flex items-center justify-between px-6 py-4">
				<!-- Brand -->
				<div class="flex items-center">
					<a
						href={localizeHref('/')}
						class="inline-flex items-center gap-3 text-inherit no-underline"
						aria-label="Restaurant Istanbul"
					>
						<enhanced:img src={logo} alt="Restaurant Istanbul" class="h-10 w-auto object-contain" />
						<span class="hidden sm:block font-serif text-2xl font-semibold tracking-[0.06em] leading-none">
							ISTANBUL
						</span>
					</a>
				</div>

				<!-- Desktop Nav -->
				<div class="hidden items-center gap-8 text-sm font-medium tracking-wide md:flex">
					<a href={localizeHref('/locations')} class={navLinkClass}>{m.nav_locations()}</a>
					<a href={localizeHref('/menu')} class={navLinkClass}>{m.nav_menu()}</a>
					<a href={localizeHref('/about')} class={navLinkClass}>{m.nav_story()}</a>
					<a href={localizeHref('/contact')} class={navLinkClass}>{m.nav_contact()}</a>

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

				<!-- Mobile Actions -->
				<div class="flex items-center gap-4 md:hidden">
					<a
						href="https://wa.me/258847131300"
						target="_blank"
						rel="noopener noreferrer"
						class="btn-primary px-4 py-2 text-xs shadow-sm"
						aria-label="Order via WhatsApp"
					>
						{m.nav_order()}
					</a>

					<!-- Mobile Menu Toggle -->
					<button
						type="button"
						class={navSolid ? 'text-gray-900' : 'text-white'}
						aria-label="Toggle navigation menu"
						aria-expanded={isMenuOpen}
						onclick={() => (isMenuOpen = !isMenuOpen)}
					>
						{#if isMenuOpen}
							<X size={24} />
						{:else}
							<Menu size={24} />
						{/if}
					</button>
				</div>
			</div>
		</div>

		{#if isMenuOpen}
			<!-- backdrop (behind top bar) -->
			<div
				class="fixed inset-0 z-20 bg-black/40 md:hidden"
				transition:fade={{ duration: 140 }}
				onclick={() => (isMenuOpen = false)}
			></div>

			<!-- Mobile Menu (fully opaque panel) -->
			<div
				class="relative z-30 border-t border-gray-100 bg-white text-gray-900 shadow-lg px-6 py-6 md:hidden"
				transition:slide={{ duration: 180 }}
			>
				<nav class="flex flex-col gap-6 text-sm font-medium tracking-wide">
					<a href={localizeHref('/locations')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_locations()}</a>
					<a href={localizeHref('/menu')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_menu()}</a>
					<a href={localizeHref('/about')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_story()}</a>
					<a href={localizeHref('/contact')} class="link-hover" onclick={() => (isMenuOpen = false)}>{m.nav_contact()}</a>

					<div class="h-[1px] w-full bg-gray-100"></div>

					<div class="flex flex-col gap-4">
						<a
							href="https://wa.me/258847131300"
							target="_blank"
							rel="noopener noreferrer"
							class="btn-primary w-full text-center shadow-sm"
							aria-label="Order via WhatsApp"
						>
							{m.nav_order()}
						</a>
					</div>
				</nav>
			</div>
		{/if}
	</div>
</header>
