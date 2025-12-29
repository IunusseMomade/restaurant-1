<script>
	import { onMount } from 'svelte';
	import { fade, slide } from 'svelte/transition';
	import { Menu, X } from '@lucide/svelte';
	import section1_1 from '$lib/assets/images/section1-1.jpeg?enhanced';
	import * as m from '$lib/paraglide/messages';
	import { localizeHref } from '$lib/paraglide/runtime';
	let isMenuOpen = $state(false);
	let isScrolled = $state(false);
	let heroReady = $state(false);

	// make the transparent gray image overlay work
	import overlayImage from '$lib/assets/images/transparent.png';
	import logo from '$lib/assets/ir-logo.png?enhanced';

	const navSolid = $derived(isScrolled || isMenuOpen);
	const navLinkClass = $derived(
		navSolid ? 'link-hover' : 'link-hover text-white/90 hover:text-white'
	);

	onMount(() => {
		const onScroll = () => {
			isScrolled = window.scrollY > 8;
		};

		onScroll();
		window.addEventListener('scroll', onScroll, { passive: true });

		// trigger hero animations after first paint
		requestAnimationFrame(() => {
			heroReady = true;
		});

		return () => window.removeEventListener('scroll', onScroll);
	});
</script>

<header class="relative flex w-full flex-col">
	<!-- Top Nav overlaying hero -->
	<div class="absolute inset-x-0 top-0 z-30">
		<div
			class={`relative z-40 ${
				isMenuOpen
					? 'bg-white text-gray-900 border-b border-gray-200' // full opacity while menu open
					: isScrolled
						? 'bg-white/95 text-gray-900 backdrop-blur border-b border-gray-200'
						: 'bg-transparent text-white border-b border-transparent'
			}`}
		>
			<!-- Main Nav Bar -->
			<div class="container mx-auto flex items-center justify-between px-6 py-4">
				<!-- Brand Logo -->
				<div class="flex items-center">
					<a
						href={localizeHref('/')}
						class="inline-flex items-center gap-3 text-inherit no-underline"
						aria-label="Restaurant Istanbul"
					>
						<enhanced:img src={logo} alt="Restaurant Istanbul" class="h-10 w-auto object-contain" />
						<span class="hidden sm:block font-serif text-2xl font-semibold tracking-[0.06em] leading-none ">
							ISTANBUL
						</span>
					</a>
				</div>

				<!-- Desktop Nav Actions -->
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
							class="btn-primary px-6 py-2.5 text-xs shadow-sm inline-block"
							aria-label="Order via WhatsApp"
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
			<!-- backdrop (must stay BEHIND the top bar) -->
			<div
				class="fixed inset-0 z-20 bg-black/40 md:hidden"
				transition:fade={{ duration: 140 }}
				onclick={() => (isMenuOpen = false)}
			></div>

			<!-- Mobile Menu (animated) -->
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
						<a href="https://wa.me/258847131300" target="_blank" rel="noopener noreferrer" class="btn-primary w-full text-center shadow-sm" aria-label="Order via WhatsApp"> {m.nav_order()} </a>
					</div>
				</nav>
			</div>
		{/if}
	</div>

	<!-- Hero Section -->
	<div class="relative h-[500px] w-full">
		<div class="absolute inset-0">
			<enhanced:img
				src={section1_1}
				alt="Luxury Dining"
				class={`h-full w-full object-cover hero-img ${heroReady ? 'is-ready' : ''}`}
			/>
			<div class="absolute inset-0 bg-gradient-to-r from-black/70 via-black/30 to-transparent"></div>
		</div>

		<div class="relative container mx-auto flex h-full items-center px-6 pt-24  md:pt-0">
			<div class={`max-w-xl text-white hero ${heroReady ? 'is-ready' : ''}`}>
				<h5 class="mb-4 text-overline text-primary hero-item hero-item-1">{m.hero_welcome()}</h5>

				<h1 class="font-serif mb-6 text-5xl leading-tight md:text-6xl hero-item hero-item-2">
					{@html m.home_header_h1_html()}
				</h1>

				<p class="mb-8 text-sm font-light leading-relaxed text-gray-200 md:text-base hero-item hero-item-3">
					{@html m.home_header_desc_html()}
				</p>

				<a
					href={localizeHref('/menu')}
					class="inline-block border border-primary bg-transparent px-8 py-3 text-overline text-white transition-all hover:bg-primary hover:text-white hero-item hero-item-4"
				>
					{m.btn_view_menu()}
				</a>
			</div>
		</div>
	</div>

	<!-- Venue Level Sub-Nav -->
	<div class="hidden w-full border-t border-b border-gray-100 bg-[#FAFAFA] py-3 md:block">
		<div class="container mx-auto flex items-center justify-between px-6">
			<h2 class="font-serif text-xl tracking-wide text-gray-800">{m.subnav_explore()}</h2>
			<div class="flex gap-8 text-overline text-gray-500">
				<a href="#overview" class="-mb-3.5 border-b-2 border-primary pb-3 text-primary"
					>{m.subnav_overview()}</a
				>
				<a href="#signature-dishes" class="transition-colors hover:text-gray-900">{m.subnav_dishes()}</a>
				<a href="#gallery" class="transition-colors hover:text-gray-900">{m.subnav_gallery()}</a>
				<a href="#membership" class="transition-colors hover:text-gray-900">{m.subnav_membership()}</a>
				<a href="#info" class="transition-colors hover:text-gray-900">{m.subnav_info()}</a>
			</div>
		</div>
	</div>
</header>

<style>
	@media (prefers-reduced-motion: reduce) {
		.hero-img,
		.hero-item {
			animation: none !important;
			transition: none !important;
			transform: none !important;
			opacity: 1 !important;
		}
	}

	/* subtle hero image zoom */
	.hero-img {
		transform: scale(1.04);
		transition: transform 900ms cubic-bezier(0.2, 0.8, 0.2, 1);
		will-change: transform;
	}
	.hero-img.is-ready {
		transform: scale(1);
	}

	/* staggered hero text reveal */
	.hero .hero-item {
		opacity: 0;
		transform: translateY(10px);
		animation: heroIn 700ms cubic-bezier(0.2, 0.8, 0.2, 1) forwards;
		will-change: transform, opacity;
	}
	.hero:not(.is-ready) .hero-item {
		animation: none;
	}
	.hero.is-ready .hero-item-1 { animation-delay: 80ms; }
	.hero.is-ready .hero-item-2 { animation-delay: 150ms; }
	.hero.is-ready .hero-item-3 { animation-delay: 220ms; }
	.hero.is-ready .hero-item-4 { animation-delay: 290ms; }

	@keyframes heroIn {
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}
</style>
