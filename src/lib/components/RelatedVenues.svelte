<script>
	import { ChevronRight, Utensils, Tag } from '@lucide/svelte';
	import * as m from '$lib/paraglide/messages';

	const menuHighlights = [{ id: 1 }, { id: 2 }, { id: 3 }];

	const name = (id) =>
		id === 1 ? m.home_specials_item_1_name() : id === 2 ? m.home_specials_item_2_name() : m.home_specials_item_3_name();

	const desc = (id) =>
		id === 1 ? m.home_specials_item_1_desc() : id === 2 ? m.home_specials_item_2_desc() : m.home_specials_item_3_desc();

	const category = (id) =>
		id === 1 ? m.home_specials_item_1_category() : id === 2 ? m.home_specials_item_2_category() : m.home_specials_item_3_category();

	const price = (id) =>
		id === 1 ? m.home_specials_item_1_price() : id === 2 ? m.home_specials_item_2_price() : m.home_specials_item_3_price();

	const images = {
		1: 'https://images.unsplash.com/photo-1604909053197-72bb2b31f3da?auto=format&fit=crop&q=80&w=600',
		2: 'https://images.unsplash.com/photo-1540189549336-e6e99c3679fe?auto=format&fit=crop&q=80&w=600',
		3: 'https://images.unsplash.com/photo-1604335399105-0f0b4f6db5ad?auto=format&fit=crop&q=80&w=600'
	};
</script>

<section id="signature-dishes" class="overflow-hidden border-t border-gray-100 bg-white py-20">
	<div class="container mx-auto mb-12 flex flex-col justify-between gap-6 px-6 md:flex-row md:items-end">
		<div class="md:w-1/3">
			<div class="mb-4 flex items-center gap-4">
				<div class="h-[1px] w-12 bg-primary"></div>
				<span class="text-overline text-gray-400">{m.home_specials_label()}</span>
			</div>

			<h3 class="font-serif text-4xl leading-tight text-gray-900">
				{@html m.home_specials_title_html()}
			</h3>
		</div>
		<div class="md:w-1/2">
			<p class="text-sm font-light leading-7 text-gray-500">
				{m.home_specials_desc()}
			</p>
		</div>
	</div>

	<div class="scrollbar-hide container mx-auto overflow-x-auto pb-10 px-6">
		<div class="flex min-w-max gap-8">
			{#each menuHighlights as item (item.id)}
				<div class="group w-[350px] cursor-pointer border border-transparent bg-white transition-all duration-300 hover:border-gray-100 hover:shadow-xl">
					<div class="relative h-[220px] overflow-hidden">
						<img
							src={images[item.id]}
							alt={name(item.id)}
							class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-105"
						/>
						<div class="absolute top-4 right-4 rounded-full bg-white/90 p-2 opacity-0 transition-opacity group-hover:opacity-100">
							<ChevronRight size={16} class="text-primary" />
						</div>
					</div>

					<div class="p-6">
						<h4 class="font-serif mb-2 text-lg text-gray-900 transition-colors group-hover:text-primary">
							{name(item.id)}
						</h4>
						<p class="mb-4 h-8 text-xs text-gray-500 line-clamp-2">{desc(item.id)}</p>

						<div class="mb-6 grid grid-cols-2 gap-y-2 text-[10px] font-bold uppercase tracking-wider text-gray-400">
							<div class="flex items-center gap-1 text-secondary">
								<Utensils size={10} class="text-primary" />
								{category(item.id)}
							</div>
							<div class="flex items-center gap-1">
								<Tag size={10} class="text-accent" />
								{price(item.id)}
							</div>
						</div>

						<div class="flex items-center justify-between border-t border-gray-100 pt-4">
							<button class="btn-primary text-[10px]">{m.home_specials_btn_order()}</button>
							<span class="text-[10px] font-bold uppercase tracking-widest text-gray-400 hover:text-gray-900">
								{m.home_specials_btn_details()}
							</span>
						</div>
					</div>
				</div>
			{/each}

			<!-- Duplicate for visual length -->
			{#each menuHighlights as item (`${item.id}-duplicate`)}
				<div class="group w-[350px] cursor-pointer border border-transparent bg-white transition-all duration-300 hover:border-gray-100 hover:shadow-xl">
					<div class="relative h-[220px] overflow-hidden">
						<img
							src={images[item.id]}
							alt={name(item.id)}
							class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-105"
						/>
					</div>
					<div class="p-6">
						<h4 class="font-serif mb-2 text-lg text-gray-900 transition-colors group-hover:text-primary">
							{name(item.id)}
						</h4>
						<p class="mb-4 h-8 text-xs text-gray-500 line-clamp-2">{desc(item.id)}</p>
						<div class="mb-6 grid grid-cols-2 gap-y-2 text-[10px] font-bold uppercase tracking-wider text-gray-400">
							<div class="flex items-center gap-1 text-secondary">
								<Utensils size={10} class="text-primary" />
								{category(item.id)}
							</div>
							<div class="flex items-center gap-1">
								<Tag size={10} class="text-accent" />
								{price(item.id)}
							</div>
						</div>
						<div class="flex items-center justify-between border-t border-gray-100 pt-4">
							<button class="btn-primary text-[10px]">{m.home_specials_btn_order()}</button>
							<span class="text-[10px] font-bold uppercase tracking-widest text-gray-400 hover:text-gray-900">
								{m.home_specials_btn_details()}
							</span>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>
