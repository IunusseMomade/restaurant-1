<script>
	import { Clock, MapPin, Wifi, Car, ShoppingBag } from '@lucide/svelte';
	import * as m from '$lib/paraglide/messages';
	import { localizeHref } from '$lib/paraglide/runtime';
</script>

<section id="info" class="border-t border-gray-100 bg-gray-50 py-12">
	<div class="container mx-auto px-6">
		<div class="mb-12 grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-4">
			<!-- Hours -->
			<div class="flex items-start gap-4 border-r border-gray-200 pr-4 last:border-0">
				<Clock class="mt-1 shrink-0 text-primary" size={20} />
				<div>
					<h4 class="mb-1 text-overline text-gray-400">{m.info_hours_label()}</h4>
					<p class="font-serif text-lg text-gray-800">{m.info_hours_value()}</p>
					<p class="mt-1 text-xs text-gray-500">{m.info_hours_sub()}</p>
				</div>
			</div>

			<!-- Locations -->
			<div class="flex items-start gap-4 border-r border-gray-200 pr-4 last:border-0">
				<MapPin class="mt-1 shrink-0 text-primary" size={20} />
				<div>
					<h4 class="mb-1 text-overline text-gray-400">{m.info_locations_label()}</h4>
					<p class="font-serif text-lg text-gray-800">{m.info_locations_value()}</p>
					<p class="mt-1 text-xs text-gray-500">{m.info_locations_sub()}</p>
				</div>
			</div>

			<!-- Amenities -->
			<div class="flex items-start gap-4 border-r border-gray-200 pr-4 last:border-0">
				<Wifi class="mt-1 shrink-0 text-primary" size={20} />
				<div>
					<h4 class="mb-1 text-overline text-gray-400">{m.info_amenities_label()}</h4>
					<p class="font-serif text-lg text-gray-800">{m.info_amenities_value()}</p>
					<p class="mt-1 text-xs text-gray-500">{m.info_amenities_sub()}</p>
				</div>
			</div>

			<!-- Convenience -->
			<div class="flex items-start gap-4">
				<ShoppingBag class="mt-1 shrink-0 text-primary" size={20} />
				<div>
					<h4 class="mb-1 text-overline text-gray-400">{m.info_convenience_label()}</h4>
					<p class="font-serif text-lg text-gray-800">{m.info_convenience_value()}</p>
					<p class="mt-1 flex items-center gap-2 text-xs text-gray-500">
						<Car size={14} class="text-primary" />
						<span>{m.info_convenience_sub()}</span>
					</p>
				</div>
			</div>
		</div>

		<div class="text-center">
			<a
				href={localizeHref('/menu')}
				class="transform btn-primary inline-block px-10 py-4 text-sm tracking-[0.15em] hover:-translate-y-0.5"
			>
				{m.info_cta_menu()}
			</a>
		</div>
	</div>
</section>
