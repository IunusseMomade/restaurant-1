<script>

	import section4_1 from '$lib/assets/images/gallery/section4-1.jpeg';
	import section4_2 from '$lib/assets/images/gallery/section4-2.jpeg';
	import section4_3 from '$lib/assets/images/gallery/section4-3.jpeg';
	import section4_4 from '$lib/assets/images/gallery/section4-4.jpeg';
	import section4_5 from '$lib/assets/images/gallery/section4-5.jpeg';


	const galleryImages = [
    {
      alt: "put seo alt",
      image: section4_1,
     
    },
	{
      alt: "put seo alt",
      image: section4_2,
     
    },
	{
      alt: "put seo alt",
      image: section4_3,
     
    },
	{
      alt: "put seo alt",
      image: section4_4,
     
    },
	{
      alt: "put seo alt",
      image: section4_5,
     
    },
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
			<enhanced:img
				src={galleryImages[0].image}
				class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
				alt="Gallery 1"
			/>
			<div class="absolute inset-0 bg-black/20 transition-colors group-hover:bg-transparent"></div>
		</div>
		<div class="group relative h-64 overflow-hidden md:col-span-1">
			<enhanced:img
				src={galleryImages[1].image}
				class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
				alt="Gallery 2"
			/>
			<div class="absolute inset-0 bg-black/20 transition-colors group-hover:bg-transparent"></div>
		</div>
		<div class="group relative h-64 overflow-hidden md:col-span-1">
			<enhanced:img
				src={galleryImages[2].image}
				class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
				alt="Gallery 3"
			/>
			<div class="absolute inset-0 bg-black/20 transition-colors group-hover:bg-transparent"></div>
		</div>

		<!-- Bottom Row Centered -->
		<div class="mt-0 flex flex-col justify-center gap-4 md:col-span-3 md:mt-2 md:flex-row md:gap-6">
			<div class="group relative h-64 overflow-hidden md:w-1/3">
				<enhanced:img
					src={galleryImages[3].image}
					class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
					alt="Gallery 4"
				/>
			</div>
			<div class="group relative h-64 overflow-hidden md:w-1/3">
				<enhanced:img
					src={galleryImages[4].image}
					class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
					alt="Gallery 5"
				/>
			</div>
		</div>
	</div>
</section>
