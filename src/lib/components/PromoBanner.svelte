<script>
	import section6_1 from '$lib/assets/images/section6-1.jpeg?enhanced';
     import { localizeHref } from '$lib/paraglide/runtime';
	import { Gift, Sparkles } from '@lucide/svelte';
	import * as m from '$lib/paraglide/messages';
</script>
<section id="membership" class="relative flex h-125 w-full items-center overflow-hidden">
	<!-- Parallax-like Background -->
	<div class="absolute inset-0">
		<enhanced:img
			src={section6_1}
			alt="Palace Background"
			class="h-full w-full object-cover"
		/>
		<!-- Gradient Overlay -->
		<div class="absolute inset-0 bg-linear-to-r from-black/50 to-transparent"></div>
	</div>

	<!-- Floating Content Card -->
	<div class="relative z-10 container mx-auto flex justify-end px-6">
		<!-- Gift Card -->
		<div
			class="relative max-w-md overflow-visible rounded-2xl border-2 border-dashed border-white/60 bg-white/90 p-10 shadow-2xl ring-1 ring-black/5 backdrop-blur md:p-12"
		>
			<!-- Ribbon badge -->
			<div class="absolute left-6 top-6 z-10 inline-flex items-center gap-2 rounded-full bg-primary px-4 py-2 text-[10px] font-bold uppercase tracking-widest text-white shadow-lg">
				<Gift size={14} />
				{m.promo_badge()}
			</div>

			<!-- Bow (top-right) -->
			<div class="absolute -top-6 right-10 z-10 flex items-center gap-2">
				<div class="h-10 w-10 rounded-full bg-primary/25 blur-[0.2px]"></div>
				<div class="h-10 w-10 rounded-full bg-secondary/25 blur-[0.2px]"></div>
				<div class="-ml-1 h-6 w-6 rotate-45 rounded-md bg-accent/25"></div>
			</div>

			<!-- Vertical ribbon strip -->
			<div class="absolute inset-y-0 right-14 w-10 bg-gradient-to-b from-primary/15 via-secondary/10 to-accent/15"></div>
			<div class="absolute inset-y-0 right-[3.35rem] w-[2px] bg-primary/25"></div>

			<!-- Decorative sparkles -->
			<div class="absolute right-6 top-20 text-secondary/40">
				<Sparkles size={18} />
			</div>

			<!-- Gift tag (bottom-left) -->
			<div class="absolute -bottom-6 -left-6 rotate-[-8deg] rounded-2xl bg-gray-900 px-5 py-4 text-white shadow-xl">
				<div class="mb-2 flex items-center gap-2">
					<span class="inline-block h-2.5 w-2.5 rounded-full bg-white/80"></span>
					<span class="text-[10px] font-bold uppercase tracking-widest text-white/80">{m.promo_tag_city()}</span>
				</div>
				<p class="text-xs font-semibold leading-tight">{m.promo_tag_discount()}</p>
				<p class="text-[10px] text-white/70">{m.promo_tag_time()}</p>
			</div>

			<!-- Content -->
			<h3 class="font-serif mb-4 mt-10 text-2xl font-bold tracking-wide text-gray-900">
				{m.promo_title()}
			</h3>

			<p class="mb-8 text-sm leading-relaxed text-gray-700">
				{@html m.promo_desc_html()}
			</p>

			<a
				href={localizeHref('/menu')}
				class="inline-flex items-center gap-2 rounded-full bg-gray-900 px-6 py-3 text-overline text-white shadow-sm transition-all hover:bg-primary"
			>
				{m.promo_btn_menu()}
				<span aria-hidden="true" class="text-white/80">→</span>
			</a>
		</div>
	</div>
</section>
