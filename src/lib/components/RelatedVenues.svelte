<script>
	import { ChevronRight, Utensils, Tag } from '@lucide/svelte';
	import * as m from '$lib/paraglide/messages';
	import { localizeHref } from '$lib/paraglide/runtime';

	// Use local enhanced images for the featured items
	import adana_kebab from '$lib/assets/images/menu/adana-kebab.jpeg?enhanced';
	import beyti_sarma from '$lib/assets/images/menu/beyti-sarma.jpeg?enhanced';
	import kasarli_kofte from '$lib/assets/images/menu/kasarli-kofte.jpeg?enhanced';

	// add the missing ones (all enhanced)
	import mix_kebab from '$lib/assets/images/menu/mix-kebab.jpeg?enhanced';
	import kebab_beringela_1 from '$lib/assets/images/menu/kebab-beringela-1.jpeg?enhanced';
	import lamb_steak from '$lib/assets/images/menu/lamb-steak.jpeg?enhanced';
	import lulas_grelhadas from '$lib/assets/images/menu/lulas-grelhadas.jpeg?enhanced';
	import prato_familiar_mariscos from '$lib/assets/images/menu/prato-familiar-mariscos.jpeg?enhanced';
	import schnitzel from '$lib/assets/images/menu/schnitzel.jpeg?enhanced';

	const priceMZN = (n) => () => `${n} MZN`;

	const featured = [
		{
			id: 'mix_kebab',
			image: mix_kebab,
			href: localizeHref('/menu#kebab'),
			name: m.item_mix_kebab_1,
			desc: m.desc_mix_kebab_1,
			category: m.cat_kebab,
			price: priceMZN(1500)
		},
		{
			id: 'adana_kebab',
			image: adana_kebab,
			href: localizeHref('/menu#kebab'),
			name: m.item_adana_spicy,
			desc: m.desc_adana_spicy,
			category: m.cat_kebab,
			price: priceMZN(900)
		},
		{
			id: 'kasarli_kofte',
			image: kasarli_kofte,
			href: localizeHref('/menu#kebab'),
			name: m.item_kasarli_kofte,
			desc: m.desc_kasarli_kofte,
			category: m.cat_kebab,
			price: priceMZN(1200)
		},
		{
			id: 'beyti_sarma',
			image: beyti_sarma,
			href: localizeHref('/menu#special'),
			name: m.item_beyti_sarma,
			desc: m.desc_beyti_sarma,
			category: m.cat_special,
			price: priceMZN(1500)
		},
		{
			id: 'kebab_beringela',
			image: kebab_beringela_1,
			href: localizeHref('/menu#special'),
			name: m.item_patlicanli_kebap,
			desc: m.desc_patlicanli_kebap,
			category: m.cat_special,
			price: priceMZN(1200)
		},
		{
			id: 'lamb_steak',
			image: lamb_steak,
			href: localizeHref('/menu#steakhouse'),
			name: m.item_lamb_steak,
			desc: m.desc_lamb_steak,
			category: m.cat_steakhouse,
			price: priceMZN(1900)
		},
		{
			id: 'lulas_grelhadas',
			image: lulas_grelhadas,
			href: localizeHref('/menu#seafood'),
			name: m.item_grilled_squid,
			desc: m.desc_grilled_squid,
			category: m.cat_seafood,
			price: priceMZN(1700)
		},
		{
			id: 'prato_familiar_mariscos',
			image: prato_familiar_mariscos,
			href: localizeHref('/menu#seafood'),
			name: m.item_seafood_family,
			desc: m.desc_seafood_family,
			category: m.cat_seafood,
			price: priceMZN(5000)
		},
		{
			id: 'schnitzel',
			image: schnitzel,
			href: localizeHref('/menu#chicken'),
			name: m.item_schnitzel,
			desc: m.desc_schnitzel,
			category: m.cat_chicken,
			price: priceMZN(800)
		}
	];
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

	<div
		class="scrollbar-hide container mx-auto overflow-x-auto pb-10 px-6 scroll-smooth snap-x snap-mandatory md:snap-none"
	>
		<div class="flex min-w-max gap-8">
			{#each featured as item (item.id)}
				<a
					href={item.href}
					class="group block shrink-0 snap-start w-[85vw] sm:w-[350px] cursor-pointer border border-transparent bg-white transition-all duration-300 hover:border-gray-100 hover:shadow-xl"
					aria-label={item.name()}
				>
					<div class="relative h-[220px] overflow-hidden">
						<enhanced:img
							src={item.image}
							alt={item.name()}
							class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-105"
						/>
						<div class="absolute top-4 right-4 rounded-full bg-white/90 p-2 opacity-0 transition-opacity group-hover:opacity-100">
							<ChevronRight size={16} class="text-primary" />
						</div>
					</div>

					<div class="p-6">
						<h4 class="font-serif mb-2 text-lg text-gray-900 transition-colors group-hover:text-primary">
							{item.name()}
						</h4>
						<p class="mb-4 h-8 text-xs text-gray-500 line-clamp-2">{item.desc()}</p>

						<div class="mb-6 grid grid-cols-2 gap-y-2 text-[10px] font-bold uppercase tracking-wider text-gray-400">
							<div class="flex items-center gap-1 text-secondary">
								<Utensils size={10} class="text-primary" />
								{item.category()}
							</div>
							<div class="flex items-center gap-1">
								<Tag size={10} class="text-accent" />
								{item.price()}
							</div>
						</div>

						<div class="flex items-center justify-between border-t border-gray-100 pt-4">
							<span class="btn-primary text-[10px]">{m.home_specials_btn_order()}</span>
							<span class="text-[10px] font-bold uppercase tracking-widest text-gray-400 hover:text-gray-900">
								{m.home_specials_btn_details()}
							</span>
						</div>
					</div>
				</a>
			{/each}
		</div>
	</div>
</section>
