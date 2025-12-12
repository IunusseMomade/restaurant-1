<script>
	import { ChevronRight, Utensils, Tag } from '@lucide/svelte';

	const menuHighlights = [
		{
			id: 1,
			name: 'THE SHAMIANA BURGER',
			image:
				'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?auto=format&fit=crop&q=80&w=600',
			desc: 'Our legendary tenderloin patty with melted cheddar and caramelized onions.',
			category: 'Mains',
			price: '$24.00'
		},
		{
			id: 2,
			name: 'TRUFFLE MUSHROOM PASTA',
			image:
				'https://images.unsplash.com/photo-1473093295043-cdd812d0e601?auto=format&fit=crop&q=80&w=600',
			desc: 'Handmade fettuccine tossed in a rich truffle cream sauce.',
			category: 'Pasta',
			price: '$28.00'
		},
		{
			id: 3,
			name: 'SICHUAN PRAWNS',
			image:
				'https://images.unsplash.com/photo-1552566626-52f8b828add9?auto=format&fit=crop&q=80&w=600',
			desc: 'Tiger prawns wok-tossed in our secret spicy Sichuan sauce.',
			category: 'Starters',
			price: '$32.00'
		}
	];
</script>

<section id="signature-dishes" class="overflow-hidden border-t border-gray-100 bg-white py-20">
	<div
		class="container mx-auto mb-12 flex flex-col justify-between gap-6 px-6 md:flex-row md:items-end"
	>
		<div class="md:w-1/3">
			<div class="mb-4 flex items-center gap-4">
				<div class="h-[1px] w-12 bg-[#C5A059]"></div>
				<span class="text-xs font-bold uppercase tracking-widest text-gray-400">On The Menu</span>
			</div>
			<h3 class="font-serif text-4xl leading-tight text-gray-900">
				SIGNATURE <br /> DISHES
			</h3>
		</div>
		<div class="md:w-1/2">
			<p class="text-sm font-light leading-7 text-gray-500">
				Explore a curated selection of our most loved dishes. From our historic burger to
				contemporary asian fusion, every bite is crafted with passion at both our Colaba and Bandra
				locations.
			</p>
		</div>
	</div>

	<!-- Carousel Container -->
	<div class="scrollbar-hide container mx-auto overflow-x-auto pb-10 px-6">
		<div class="flex min-w-max gap-8">
			{#each menuHighlights as item (item.id)}
				<div
					class="group w-[350px] cursor-pointer border border-transparent bg-white transition-all duration-300 hover:border-gray-100 hover:shadow-xl"
				>
					<div class="relative h-[220px] overflow-hidden">
						<img
							src={item.image}
							alt={item.name}
							class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-105"
						/>
						<div
							class="absolute top-4 right-4 rounded-full bg-white/90 p-2 opacity-0 transition-opacity group-hover:opacity-100"
						>
							<ChevronRight size={16} class="text-[#C5A059]" />
						</div>
					</div>
					<div class="p-6">
						<h4
							class="font-serif mb-2 text-lg text-gray-900 transition-colors group-hover:text-[#C5A059]"
						>
							{item.name}
						</h4>
						<p class="mb-4 h-8 text-xs text-gray-500 line-clamp-2">{item.desc}</p>

						<div
							class="mb-6 grid grid-cols-2 gap-y-2 text-[10px] font-bold uppercase tracking-wider text-gray-400"
						>
							<div class="flex items-center gap-1">
								<Utensils size={10} class="text-[#C5A059]" />
								{item.category}
							</div>
							<div class="flex items-center gap-1">
								<Tag size={10} class="text-[#C5A059]" />
								{item.price}
							</div>
						</div>

						<div class="flex items-center justify-between border-t border-gray-100 pt-4">
							<button
								class="bg-[#C5A059] px-4 py-2 text-[10px] font-bold uppercase tracking-widest text-white hover:bg-[#967941]"
							>
								Order Now
							</button>
							<span
								class="text-[10px] font-bold uppercase tracking-widest text-gray-400 hover:text-gray-900"
							>
								Details +
							</span>
						</div>
					</div>
				</div>
			{/each}
			<!-- Duplicate for visual length -->
			{#each menuHighlights as item (`${item.id}-duplicate`)}
				<div
					class="group w-[350px] cursor-pointer border border-transparent bg-white transition-all duration-300 hover:border-gray-100 hover:shadow-xl"
				>
					<div class="relative h-[220px] overflow-hidden">
						<img
							src={item.image}
							alt={item.name}
							class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-105"
						/>
					</div>
					<div class="p-6">
						<h4
							class="font-serif mb-2 text-lg text-gray-900 transition-colors group-hover:text-[#C5A059]"
						>
							{item.name}
						</h4>
						<p class="mb-4 h-8 text-xs text-gray-500 line-clamp-2">{item.desc}</p>
						<div
							class="mb-6 grid grid-cols-2 gap-y-2 text-[10px] font-bold uppercase tracking-wider text-gray-400"
						>
							<div class="flex items-center gap-1">
								<Utensils size={10} class="text-[#C5A059]" />
								{item.category}
							</div>
							<div class="flex items-center gap-1">
								<Tag size={10} class="text-[#C5A059]" />
								{item.price}
							</div>
						</div>
						<div class="flex items-center justify-between border-t border-gray-100 pt-4">
							<button
								class="bg-[#C5A059] px-4 py-2 text-[10px] font-bold uppercase tracking-widest text-white hover:bg-[#967941]"
								>Order Now</button
							>
							<span
								class="text-[10px] font-bold uppercase tracking-widest text-gray-400 hover:text-gray-900"
								>Details +</span
							>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>
