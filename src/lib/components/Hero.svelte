<script>
	import { Share2 } from '@lucide/svelte';
	      import section2_1 from '$lib/assets/images/section2-1.jpeg?enhanced';
</script>

<section id="overview" class="container relative mx-auto px-6 py-16 md:py-20">
	<div class="absolute top-10 right-10 hidden text-primary lg:block">
		<div class="rounded-full border border-primary p-2">
			<Share2 size={16} />
		</div>
	</div>

	<!-- Title Block -->
	<div class="mx-auto mb-16 max-w-3xl text-center">
		<div class="mx-auto mb-6 h-[1px] w-16 bg-primary"></div>
		<h1 class="font-serif mb-6 text-4xl leading-tight text-gray-900 md:text-6xl">
			MUMBAI'S FIRST <br />
			<span class="italic">COFFEE SHOP</span>
		</h1>
		<p class="mx-auto max-w-2xl text-sm font-light leading-relaxed text-gray-500 md:text-base">
			Founded in 1973 as a coffee shop, Shamiana offers an all-day dining experience with an
			international à la carte menu, breakfast buffet, and Mumbai's most delicious weekend brunch.
		</p>
	</div>

	<!-- Split Content Grid -->
	<div class="grid grid-cols-1 items-center gap-12 lg:grid-cols-2 lg:gap-20">
		<!-- Left: Image -->
		<div class="group relative overflow-hidden">
			<!-- <img
				src="https://images.unsplash.com/photo-1473093295043-cdd812d0e601?auto=format&fit=crop&q=80&w=1200"
				alt="Signature Pasta Dish"
				class="h-[400px] w-full transform object-cover transition-transform duration-700 ease-out group-hover:scale-105"
			/> -->
			<enhanced:img
				src={section2_1}
				alt="signature image"
				class="h-100 w-full object-cover"
			/>
			 
		</div>

		<!-- Right: Text Content -->
		<div class="flex h-full flex-col justify-center">
			<h2 class="font-serif relative mb-6 text-3xl text-gray-800 md:text-4xl">
				<span class="mr-3 text-primary">—</span>
				EFFORTLESS <br /> ICONIC ALL-DAY <br /> DINING
			</h2>
			<p class="mb-6 text-sm font-light leading-7 text-gray-500">
				Step into Shamiana, where illustrious history meets modern comfort. From the legendary
				Shamiana Burger to our authentic local delicacies, every dish tells a story of Mumbai's
				culinary heritage combined with world-class hospitality.
			</p>

			<div class="space-y-2">
				<div class="flex items-center gap-2 text-sm text-gray-600">
					<span class="h-1.5 w-1.5 rounded-full bg-primary"></span>
					<span>Signature Weekend Brunch</span>
				</div>
				<div class="flex items-center gap-2 text-sm text-gray-600">
					<span class="h-1.5 w-1.5 rounded-full bg-primary"></span>
					<span>Live Music Evenings</span>
				</div>
				<div class="flex items-center gap-2 text-sm text-gray-600">
					<span class="h-1.5 w-1.5 rounded-full bg-primary"></span>
					<span>Al Fresco Seating Available</span>
				</div>
			</div>
		</div>
	</div>
</section>
