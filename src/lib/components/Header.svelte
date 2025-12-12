<script>
	import { Menu, X } from '@lucide/svelte';

	let isMenuOpen = $state(false);
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
			<a href="/locations" class="transition-colors hover:text-[#C5A059]">LOCATIONS</a>
			<a href="/menu" class="transition-colors hover:text-[#C5A059]">MENU</a>
			<a href="/about" class="transition-colors hover:text-[#C5A059]">OUR STORY</a>
			<a href="/contact" class="transition-colors hover:text-[#C5A059]">CONTACT</a>

			<div class="ml-4 flex items-center gap-4">
				<a href="/login" class="border-b border-gray-800 pb-0.5 text-xs uppercase">Account</a>
				<button
					class="bg-[#C5A059] px-6 py-2.5 text-xs font-bold uppercase tracking-widest text-white shadow-sm transition-colors hover:bg-[#a68545]"
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

	<!-- Hero Section -->
	<div class="relative h-[500px] w-full">
		<div class="absolute inset-0">
			<img
				src="https://images.unsplash.com/photo-1514362545857-3bc16c4c7d1b?auto=format&fit=crop&q=80&w=1920"
				alt="Luxury Dining"
				class="h-full w-full object-cover"
			/>
			<div class="absolute inset-0 bg-gradient-to-r from-black/70 via-black/30 to-transparent"></div>
		</div>
		<div class="relative container mx-auto flex h-full items-center px-6">
			<div class="max-w-xl text-white">
				<h5 class="mb-4 text-xs font-bold uppercase tracking-[0.2em] text-[#C5A059]">
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
					class="border border-[#C5A059] bg-transparent px-8 py-3 text-xs font-bold uppercase tracking-widest text-white transition-all hover:bg-[#C5A059] hover:text-white"
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
			<div class="flex gap-8 text-xs font-bold uppercase tracking-widest text-gray-500">
				<a href="#overview" class="-mb-3.5 border-b-2 border-[#C5A059] pb-3 text-[#C5A059]"
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
