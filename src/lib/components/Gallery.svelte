<script>
	const galleryImages = [
		'https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?auto=format&fit=crop&q=80&w=800', // Burger/Food
		'https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&q=80&w=800', // Interior 1
		'https://images.unsplash.com/photo-1559339352-11d035aa65de?auto=format&fit=crop&q=80&w=800', // Interior 2
		'https://images.unsplash.com/photo-1550966871-3ed3c47e2ce2?auto=format&fit=crop&q=80&w=800', // Interior 3
		'https://images.unsplash.com/photo-1551218808-94e220e084d2?auto=format&fit=crop&q=80&w=800' // Food close up
	];
</script>

<section id="gallery" class="container mx-auto px-6 py-20">
	<div class="mb-12 flex items-center justify-center gap-6">
		<div class="h-[1px] w-16 bg-gray-300 md:w-24"></div>
		<h3 class="font-serif text-3xl uppercase tracking-widest text-gray-800">Gallery</h3>
		<div class="h-[1px] w-16 bg-gray-300 md:w-24"></div>
	</div>

	<div class="grid grid-cols-1 gap-4 md:grid-cols-3 md:gap-6">
		<!-- Top Row -->
		<div class="group relative h-64 overflow-hidden md:col-span-1">
			<img
				src={galleryImages[0]}
				class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
				alt="Gallery 1"
			/>
			<div class="absolute inset-0 bg-black/20 transition-colors group-hover:bg-transparent"></div>
		</div>
		<div class="group relative h-64 overflow-hidden md:col-span-1">
			<img
				src={galleryImages[1]}
				class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
				alt="Gallery 2"
			/>
			<div class="absolute inset-0 bg-black/20 transition-colors group-hover:bg-transparent"></div>
		</div>
		<div class="group relative h-64 overflow-hidden md:col-span-1">
			<img
				src={galleryImages[2]}
				class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
				alt="Gallery 3"
			/>
			<div class="absolute inset-0 bg-black/20 transition-colors group-hover:bg-transparent"></div>
		</div>

		<!-- Bottom Row Centered -->
		<div class="mt-0 flex flex-col justify-center gap-4 md:col-span-3 md:mt-2 md:flex-row md:gap-6">
			<div class="group relative h-64 overflow-hidden md:w-1/3">
				<img
					src={galleryImages[3]}
					class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
					alt="Gallery 4"
				/>
			</div>
			<div class="group relative h-64 overflow-hidden md:w-1/3">
				<img
					src={galleryImages[4]}
					class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
					alt="Gallery 5"
				/>
			</div>
		</div>
	</div>
</section>
