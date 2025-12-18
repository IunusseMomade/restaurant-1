<script>
	import { Instagram, Facebook, Twitter } from '@lucide/svelte';
	import * as m from '$lib/paraglide/messages';
</script>

<footer class="border-t-[3px] border-primary bg-[#0a0a0a] pt-20 pb-8 text-white">
	<div class="container mx-auto px-6">
		<div class="mb-16 flex flex-col items-start justify-between gap-10 md:flex-row">
			<div class="max-w-sm">
				<div class="font-serif mb-2 text-2xl tracking-widest">ISTANBUL RESTAURANT</div>
				<div class="mb-6 text-[10px] uppercase tracking-widest text-gray-400">
					{m.footer_locations_line()}
				</div>
				<h5 class="mb-4 text-overline text-gray-400">
					{m.footer_subscribe_title()}
				</h5>
				<div class="flex border-b border-gray-700 pb-2">
					<input
						type="email"
						placeholder={m.footer_email_placeholder()}
						class="w-full border-none bg-transparent text-sm text-white placeholder-gray-600 outline-none"
					/>
					<button class="text-overline text-primary"
						>{m.footer_subscribe_btn()}</button
					>
				</div>
			</div>

			<!-- Links Grid -->
			<div
				class="grid grid-cols-2 gap-x-12 gap-y-8 text-xs font-light leading-loose text-gray-400 md:grid-cols-4"
			>
				<div>
					<h6 class="mb-4 text-[10px] font-bold uppercase tracking-wider text-white">{m.footer_col_about()}</h6>
					<ul class="space-y-1">
						<li class="cursor-pointer hover:text-primary">{m.footer_link_story()}</li>
						<li class="cursor-pointer hover:text-primary">{m.footer_link_chefs()}</li>
						<li class="cursor-pointer hover:text-primary">{m.footer_link_sourcing()}</li>
						<li class="cursor-pointer hover:text-primary">{m.footer_link_careers()}</li>
					</ul>
				</div>
				<div>
					<h6 class="mb-4 text-[10px] font-bold uppercase tracking-wider text-white">{m.footer_col_support()}</h6>
					<ul class="space-y-1">
						<li class="cursor-pointer hover:text-primary">{m.footer_link_contact()}</li>
						<li class="cursor-pointer hover:text-primary">{m.footer_link_faqs()}</li>
						<li class="cursor-pointer hover:text-primary">{m.footer_link_sitemap()}</li>
						<li class="cursor-pointer hover:text-primary">{m.footer_link_gift()}</li>
					</ul>
				</div>
				<div>
					<h6 class="mb-4 text-[10px] font-bold uppercase tracking-wider text-white">{m.footer_col_legal()}</h6>
					<ul class="space-y-1">
						<li class="cursor-pointer hover:text-primary">{m.footer_link_terms()}</li>
						<li class="cursor-pointer hover:text-primary">{m.footer_link_privacy()}</li>
						<li class="cursor-pointer hover:text-primary">{m.footer_link_accessibility()}</li>
					</ul>
				</div>
				<div>
					<h6 class="mb-4 text-[10px] font-bold uppercase tracking-wider text-white">{m.footer_col_social()}</h6>
					<div class="mt-2 flex gap-4">
						<Instagram size={18} class="cursor-pointer hover:text-brand-cyan" />
						<Facebook size={18} class="cursor-pointer hover:text-brand-cyan" />
						<Twitter size={18} class="cursor-pointer hover:text-brand-cyan" />
					</div>
				</div>
			</div>
		</div>

		<!-- Bottom Row: Logos & Copyright -->
		<div
			class="flex flex-col items-center justify-between gap-6 border-t border-gray-900 pt-8 md:flex-row"
		>
			<div
				class="flex flex-wrap justify-center gap-6 opacity-50 grayscale transition-all duration-500 hover:grayscale-0"
			>
				<!-- Payment Methods or Partners -->
				<span class="font-sans text-xs font-bold tracking-widest">VISA</span>
				<span class="font-sans text-xs font-bold tracking-widest">MASTERCARD</span>
				<span class="font-sans text-xs font-bold tracking-widest">AMEX</span>
				<span class="font-sans text-xs font-bold tracking-widest">UPI</span>
			</div>

			<div class="text-center text-[10px] uppercase tracking-widest text-gray-600 md:text-right">
				{m.footer_copyright()}
			</div>
		</div>
	</div>
</footer>
