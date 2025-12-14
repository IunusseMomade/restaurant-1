<script>
	import section6_1 from '$lib/assets/images/section6-1.jpeg?enhanced';
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
		<div class="relative max-w-md overflow-hidden bg-white p-10 border border-gray-200 md:p-12">
			<!-- Decorative Background blob -->
			<div
				class="absolute -top-10 -right-10 h-40 w-40 rounded-full bg-accent/10 opacity-50 blur-3xl"
			></div>

			<h3
				class="font-serif mb-4 text-2xl font-bold tracking-wide text-transparent bg-clip-text bg-gradient-to-r from-secondary to-brand-cyan"
			>
				Presente Especial
			</h3>

			<!-- Fazer design disso -->
			<p class="mb-8 text-sm leading-relaxed text-gray-600">
				Desconto de 20% em todos produtos entre 12:00 e 15:00 de segunda a sexta
				No Maputo shopping center e no Baia-Mall
			</p>
			<a
				href="/menu"
				class="inline-block border-b border-gray-800 pb-1 text-overline text-gray-800 transition-colors hover:border-primary hover:text-primary"
			>
				Ver Menu
			</a>
		</div>
	</div>
</section>
