<script>
	import { MapPin, Moon } from '@lucide/svelte';
	import HeaderSimple from '$lib/components/HeaderSimple.svelte';
	import Footer from '$lib/components/Footer.svelte';
	import location_msc from '$lib/assets/images/location-msc.jpeg?enhanced';
	import location_bm from '$lib/assets/images/section1-1.jpeg?enhanced';
	import * as m from '$lib/paraglide/messages';
</script>

<HeaderSimple />

<div class="min-h-[60vh] bg-white py-20">
	<div class="container mx-auto px-6">
		<div class="mb-16 text-center">
			<h1 class="mb-4 font-serif text-4xl">{m.locations_title()}</h1>
			<p class="mx-auto max-w-2xl text-gray-600">
				{m.locations_intro()}
			</p>
			<div
				class="mt-4 inline-flex items-center gap-2 rounded-full border border-green-100 bg-green-50 px-4 py-1 text-sm font-medium text-green-700"
			>
				<Moon size={14} />
				<span>{m.locations_badge_halal()}</span>
			</div>
		</div>

		<div class="mx-auto grid max-w-5xl gap-8 md:grid-cols-2">
			<!-- Location 1 -->
			<div class="rounded-lg border border-gray-200 bg-white overflow-hidden">
				<div class="group h-64 overflow-hidden">
					<enhanced:img
						src={location_msc}
						alt="Maputo Shopping Center"
						class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
					/>
				</div>
				<div class="p-8">
					<h3 class="mb-2 font-serif text-2xl">Maputo Shopping Center</h3>
					<div class="mb-6 flex items-start gap-3 text-gray-600">
						<MapPin class="mt-1 shrink-0 text-primary" size={18} />
						<p>Rua Ngungunhane, 85<br />Loja G 25 R/C<br />Maputo</p>
					</div>
					<a
						href="https://maps.google.com/?q=Maputo+Shopping+Center"
						target="_blank"
						rel="noopener noreferrer"
						class="group flex w-full items-center justify-center gap-2 rounded-full border border-gray-200 px-5 py-3 text-xs font-bold uppercase tracking-widest text-gray-900 transition-all hover:border-primary hover:bg-primary/5"
					>
						{m.locations_get_directions()}
					</a>
				</div>
			</div>

			<!-- Location 2 -->
			<div class="rounded-lg border border-gray-200 bg-white overflow-hidden">
				<div class="group h-64 overflow-hidden">
					<enhanced:img
						src={location_bm}
						alt="Baía-Mall"
						class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
					/>
				</div>
				<div class="p-8">
					<h3 class="mb-2 font-serif text-2xl">Baía-Mall</h3>
					<div class="mb-6 flex items-start gap-3 text-gray-600">
						<MapPin class="mt-1 shrink-0 text-primary" size={18} />
						<p>Baía Mall Shopping Center<br />Maputo<br />Mozambique</p>
					</div>
					<a
						href="https://maps.google.com/?q=Baia+Mall+Maputo"
						target="_blank"
						rel="noopener noreferrer"
						class="group flex w-full items-center justify-center gap-2 rounded-full border border-gray-200 px-5 py-3 text-xs font-bold uppercase tracking-widest text-gray-900 transition-all hover:border-primary hover:bg-primary/5"
					>
						{m.locations_get_directions()}
					</a>
				</div>
			</div>
		</div>
	</div>
</div>

<Footer />
