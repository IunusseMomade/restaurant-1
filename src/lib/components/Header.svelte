<script>
	import { Menu, X } from '@lucide/svelte';
	import section1_1 from '$lib/assets/images/section1-1.jpeg?enhanced';
	let isMenuOpen = $state(false);
	// make the transparent gray image overlay work
	import overlayImage from '$lib/assets/images/transparent.png';
</script>

<header class="flex w-full flex-col border-b border-gray-200">
	<!-- Main Nav Bar -->
	<div class="container mx-auto flex items-center justify-between px-6 py-4">
		<!-- Brand Logo Placeholder -->
		<div class="flex items-center gap-2">
			<div class="font-serif text-3xl font-bold tracking-wider">SHAMIANA</div>
			<div class="mx-2 h-8 w-[1px] bg-gray-300"></div>
			<div class="text-xs leading-tight uppercase tracking-[0.2em] text-gray-500">
				Est.<br />1973<br />Mumbai
			</div>
		</div>

		<!-- Desktop Nav Actions -->
		<div class="hidden items-center gap-8 text-sm font-medium tracking-wide md:flex">
			<a href="/locations" class="link-hover">LOCATIONS</a>
			<a href="/menu" class="link-hover">MENU</a>
			<a href="/about" class="link-hover">OUR STORY</a>
			<a href="/contact" class="link-hover">CONTACT</a>

			<div class="ml-4 flex items-center gap-4">
				<a href="/login" class="border-b border-secondary pb-0.5 text-xs uppercase text-secondary hover:text-primary hover:border-primary transition-colors">Account</a>
				<button
					class="btn-primary px-6 py-2.5 text-xs shadow-sm"
				>
					Order Online
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
				<a href="/locations" class="link-hover" onclick={() => (isMenuOpen = false)}>LOCATIONS</a>
				<a href="/menu" class="link-hover" onclick={() => (isMenuOpen = false)}>MENU</a>
				<a href="/about" class="link-hover" onclick={() => (isMenuOpen = false)}>OUR STORY</a>
				<a href="/contact" class="link-hover" onclick={() => (isMenuOpen = false)}>CONTACT</a>
				<div class="h-[1px] w-full bg-gray-100"></div>
				<div class="flex flex-col gap-4">
					<a
						href="/login"
						class="w-fit border-b border-secondary pb-0.5 text-xs uppercase text-secondary transition-colors hover:border-primary hover:text-primary"
						onclick={() => (isMenuOpen = false)}>Account</a
					>
					<button class="btn-primary w-full text-center shadow-sm"> Order Online </button>
				</div>
			</nav>
		</div>
	{/if}

	<!-- Hero Section -->
	<div class="relative h-[500px] w-full">
		<div class="absolute inset-0">
			<!-- <img
				src="https://images.unsplash.com/photo-1514362545857-3bc16c4c7d1b?auto=format&fit=crop&q=80&w=1920"
				alt="Luxury Dining"
				class="h-full w-full object-cover"
			/> -->
			<enhanced:img
				src={section1_1}
				alt="Luxury Dining"
				class="h-full w-full object-cover"
			/>
			 <!-- Transparent overlay image (on top of the main image) -->
			<!-- <div class="absolute inset-0 pointer-events-none">
			<img
				src={overlayImage}
				alt=""
				class="w-full h-full object-cover"
				aria-hidden="true"
			/>
			</div> -->
			<div class="absolute inset-0 bg-gradient-to-r from-black/70 via-black/30 to-transparent"></div>
		</div>
		<div class="relative container mx-auto flex h-full items-center px-6">
			<div class="max-w-xl text-white">
				<h5 class="mb-4 text-overline text-primary">
					Welcome to Shamiana
				</h5>
				<h1 class="font-serif mb-6 text-5xl leading-tight md:text-6xl">
					Experience <br /> <span class="italic">Timeless Taste</span>
				</h1>
				<p class="mb-8 text-sm font-light leading-relaxed text-gray-200 md:text-base">
					Indulge in an exquisite culinary journey where heritage meets contemporary elegance at our
					two iconic locations.
				</p>
				<button
					class="border border-primary bg-transparent px-8 py-3 text-overline text-white transition-all hover:bg-primary hover:text-white"
				>
					View Menu
				</button>
			</div>
		</div>
	</div>

	<!-- Venue Level Sub-Nav -->
	<div class="hidden w-full border-t border-b border-gray-100 bg-[#FAFAFA] py-3 md:block">
		<div class="container mx-auto flex items-center justify-between px-6">
			<h2 class="font-serif text-xl tracking-wide text-gray-800">EXPLORE</h2>
			<div class="flex gap-8 text-overline text-gray-500">
				<a href="#overview" class="-mb-3.5 border-b-2 border-primary pb-3 text-primary"
					>Overview</a
				>
				<a href="#signature-dishes" class="transition-colors hover:text-gray-900">Dishes</a>
				<a href="#gallery" class="transition-colors hover:text-gray-900">Gallery</a>
				<a href="#membership" class="transition-colors hover:text-gray-900">Membership</a>
				<a href="#info" class="transition-colors hover:text-gray-900">Info</a>
			</div>
		</div>
	</div>
</header>
