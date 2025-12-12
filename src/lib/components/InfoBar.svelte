<script>
	import { Clock, Utensils, MapPin, Mail, Phone } from '@lucide/svelte';
</script>

<section id="info" class="border-t border-gray-100 bg-gray-50 py-12">
	<div class="container mx-auto px-6">
		<div class="mb-12 grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-4">
			<!-- Item 1 -->
			<div class="flex items-start gap-4 border-r border-gray-200 pr-4 last:border-0">
				<Clock class="mt-1 shrink-0 text-[#C5A059]" size={20} />
				<div>
					<h4 class="mb-1 text-xs font-bold uppercase tracking-wider text-gray-400">
						Service Hours
					</h4>
					<p class="font-serif text-lg text-gray-800">Daily 7AM - 11PM</p>
					<p class="mt-1 text-xs text-gray-500">Breakfast: 7am - 11am</p>
				</div>
			</div>

			<!-- Item 2 -->
			<div class="flex items-start gap-4 border-r border-gray-200 pr-4 last:border-0">
				<Utensils class="mt-1 shrink-0 text-[#C5A059]" size={20} />
				<div>
					<h4 class="mb-1 text-xs font-bold uppercase tracking-wider text-gray-400">Cuisine</h4>
					<p class="font-serif text-lg text-gray-800">Multi-Cuisine</p>
					<p class="mt-1 text-xs text-gray-500">International & Local</p>
				</div>
			</div>

			<!-- Item 3 -->
			<div class="flex items-start gap-4 border-r border-gray-200 pr-4 last:border-0">
				<MapPin class="mt-1 shrink-0 text-[#C5A059]" size={20} />
				<div>
					<h4 class="mb-1 text-xs font-bold uppercase tracking-wider text-gray-400">Locations</h4>
					<p class="font-serif text-lg text-gray-800">Colaba & Bandra</p>
					<p class="mt-1 text-xs text-gray-500">View both locations on map</p>
				</div>
			</div>

			<!-- Item 4 -->
			<div class="flex items-start gap-4">
				<div class="flex w-full flex-col gap-3">
					<div class="flex items-center gap-2 text-xs text-gray-500">
						<Mail size={14} class="text-[#C5A059]" />
						<span>hello@shamiana.com</span>
					</div>
					<div class="flex items-center gap-2 text-xs text-gray-500">
						<Phone size={14} class="text-[#C5A059]" />
						<span>+91 22 6665 3366</span>
					</div>
				</div>
			</div>
		</div>

		<div class="text-center">
			<button
				class="transform bg-[#C5A059] px-10 py-4 text-sm font-bold uppercase tracking-[0.15em] text-white shadow-md transition-all hover:-translate-y-0.5 hover:bg-[#a68545] hover:shadow-lg"
			>
				Order Now
			</button>
		</div>
	</div>
</section>
