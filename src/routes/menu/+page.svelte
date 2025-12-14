<script>
	import HeaderSimple from '$lib/components/HeaderSimple.svelte';
import ImageViewer from '$lib/components/ImageViewer.svelte';
	import {
		Clock,
		MapPin,
		Phone,
		ChevronRight,
		Instagram,
		Facebook,
		Twitter,
		Mail,
		Menu as MenuIcon,
		X,
		Share2,
		Search,
		ChevronDown
	} from '@lucide/svelte';

	let isMenuOpen = $state(false);
	let activeCategory = $state('starters');
	let selectedImages = $state(null);

	// --- Menu Data Structure ---
	const menuCategories = [
		{ id: 'starters', label: 'Meze & Starters' },
		{ id: 'grills', label: 'Charcoal Grills' },
		{ id: 'steaks', label: 'Signature Steaks' },
		{ id: 'desserts', label: 'Desserts & Tea' }
	];

	//menu imports
	import baklava from '$lib/assets/images/menu/baklava-1.jpeg?enhanced';

	const menuItems = {
		starters: [
			{ 
				name: "Hummus with Pine Nuts", 
				desc: "Chickpeas, tahini, garlic, lemon, topped with butter-toasted pine nuts.", 
				price: "450", 
				dietary: "V", 
				image: "https://images.unsplash.com/photo-1637949385162-e416fb15b2ce?auto=format&fit=crop&q=80&w=200",
				images: [
					"https://images.unsplash.com/photo-1637949385162-e416fb15b2ce?auto=format&fit=crop&q=80&w=1200",
					"https://images.unsplash.com/photo-1577303935007-0d306ee638cf?auto=format&fit=crop&q=80&w=1200",
					"https://images.unsplash.com/photo-1623428187969-5da2dcea5ebf?auto=format&fit=crop&q=80&w=1200"
				]
			},
			{ name: "Babagannush", desc: "Smoked eggplant puree with garlic yogurt and olive oil.", price: "450", dietary: "V" },
			{ name: "Gavurdagi Salad", desc: "Finely chopped tomatoes, walnuts, pomegranate molasses, extra virgin olive oil.", price: "550", dietary: "VN", image: "https://images.unsplash.com/photo-1529312266912-b33cf6227e24?auto=format&fit=crop&q=80&w=200" },
			{ name: "Icli Kofte (Kibbeh)", desc: "Bulgur wheat shells filled with minced lamb, walnuts and spices.", price: "650", dietary: "" },
			{ name: "Calamari Tava", desc: "Crispy fried fresh calamari served with tarator sauce.", price: "850", dietary: "S", image: "https://images.unsplash.com/photo-1604909052743-94e838986d24?auto=format&fit=crop&q=80&w=200" },
			{ name: "Shrimp Guvec", desc: "Shrimp casserole with garlic, mushrooms, peppers and melted cheese.", price: "950", dietary: "S" },
		],
		grills: [
			{ 
				name: "Adana Kebab", 
				desc: "Hand-minced lamb mounted on a wide iron skewer, grilled over charcoal.", 
				price: "1200", 
				dietary: "", 
				image: "https://images.unsplash.com/photo-1603360946369-dc9bb6f54262?auto=format&fit=crop&q=80&w=200",
				images: [
					"https://images.unsplash.com/photo-1603360946369-dc9bb6f54262?auto=format&fit=crop&q=80&w=1200",
					"https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&q=80&w=1200"
				]
			},
			{ name: "Lamb Chops (Pirzola)", desc: "Four tender lamb chops marinated in fresh herbs and grilled.", price: "1600", dietary: "", image: "https://images.unsplash.com/photo-1600891964092-4316c288032e?auto=format&fit=crop&q=80&w=200" },
			{ name: "Chicken Shish", desc: "Marinated cubes of chicken breast grilled on skewers.", price: "1100", dietary: "" },
			{ name: "Istanbul Mix Grill", desc: "A platter of Adana kebab, lamb shish, chicken shish, and lamb chops.", price: "2800", dietary: "Share" },
			{ name: "Ali Nazik", desc: "Smoked eggplant puree with yoghurt, topped with sautéed lamb cubes.", price: "1450", dietary: "" },
		],
		steaks: [
			{ name: "Dry Aged Ribeye", desc: "28-day dry aged ribeye steak, grilled to perfection over charcoal.", price: "2200", dietary: "", image: "https://images.unsplash.com/photo-1558030006-450675393462?auto=format&fit=crop&q=80&w=200" },
			{ name: "Istanbul T-Bone", desc: "450g T-Bone steak served with roast potatoes and seasonal vegetables.", price: "2400", dietary: "" },
			{ name: "Beef Tenderloin", desc: "Premium tenderloin fillet, extremely tender and lean.", price: "2100", dietary: "" },
			{ name: "Lamb Cage (Kafes)", desc: "Full rack of lamb, roasted whole. Carved tableside.", price: "4500", dietary: "Share", image: "https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&q=80&w=200" },
			{ name: "Lokum (Delight)", desc: "Sliced beef fillet cooked in butter, served on hot plate.", price: "2300", dietary: "" },
		],
		desserts: [
			{ name: "Pistachio Baklava", desc: "Layers of phyllo pastry filled with Antep pistachios and syrup. Served with ice cream.", price: "650", dietary: "N", image: "https://images.unsplash.com/photo-1519676867240-f03562e64548?auto=format&fit=crop&q=80&w=200" },
			{ name: "Kunefe", desc: "Shredded pastry with melted cheese, soaked in syrup and topped with pistachios.", price: "750", dietary: "N" },
			{ name: "Sutlac", desc: "Traditional oven-baked rice pudding.", price: "450", dietary: "V" },
			{ name: "Turkish Tea", desc: "Classic black tea served in traditional glass.", price: "150", dietary: "V", image: "https://images.unsplash.com/photo-1596710629170-e6d93511c97b?auto=format&fit=crop&q=80&w=200" },
		]
	};

	const scrollToSection = (id) => {
		activeCategory = id;
		const element = document.getElementById(id);
		if (element) {
			element.scrollIntoView({ behavior: 'smooth', block: 'start' });
		}
	};
</script>

<svelte:head>
	<link href="https://fonts.googleapis.com/css2?family=Lato:wght@300;400;700&family=Playfair+Display:ital,wght@0,400;0,500;0,600;0,700;1,400&display=swap" rel="stylesheet">
</svelte:head>



<div class="min-h-screen bg-white text-gray-800 font-sans selection:bg-[#C5A059] selection:text-white">
	
	
	<!-- --- 1. HEADER (Consistent) --- -->
	 <HeaderSimple/>
	

	<!-- --- 2. HERO SECTION --- -->
	<section class="relative w-full h-[60vh] flex items-center justify-center overflow-hidden">
		<div class="absolute inset-0">
			<img 
				src="https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&q=80&w=2000" 
				alt="Steak grilling" 
				class="w-full h-full object-cover"
			/>
			<div class="absolute inset-0 bg-black/50"></div>
		</div>
		<div class="relative z-10 text-center text-white p-6 animate-fade-in-up">
			<span class="text-[#C5A059] text-xs font-bold uppercase tracking-[0.3em] mb-4 block">Taste of Bosphorus</span>
			<h1 class="font-serif text-5xl md:text-7xl mb-6">Culinary Delights</h1>
			<p class="max-w-xl mx-auto text-gray-200 font-light text-sm md:text-base leading-relaxed">
				A journey through the rich heritage of Ottoman cuisine, featuring dry-aged steaks and authentic charcoal grills.
			</p>
		</div>
	</section>

	<!-- --- 3. MENU CONTENT --- -->
	<div class="container mx-auto px-6 py-20 max-w-5xl">
		
		<!-- --- STARTERS SECTION --- -->
		<div id="starters" class="mb-24 scroll-mt-32">
			<div class="text-center mb-12">
				<span class="text-[#C5A059] text-4xl block mb-2">~</span>
				<h2 class="font-serif text-4xl text-gray-900 uppercase tracking-wide">Meze & Starters</h2>
				<p class="text-gray-500 text-sm italic mt-2">The perfect way to begin your feast</p>
			</div>
			
			<div class="grid grid-cols-1 md:grid-cols-2 gap-x-16 gap-y-10">
				{#each menuItems.starters as item}
					<div class="group flex gap-4 items-start">
						{#if item.image}
							<button 
								type="button"
								onclick={() => selectedImages = item.images || [item.image]} 
								class="shrink-0 bg-transparent border-none p-0 cursor-pointer" 
								aria-label="View full image"
							>
								<img src={item.image} alt={item.name} class="w-20 h-20 object-cover rounded-sm shadow-md hover:opacity-80 transition-opacity" />
							</button>
						{/if}
						<div class="flex-1">
							<div class="flex justify-between items-baseline mb-2 border-b border-dotted border-gray-300 pb-1">
								<h3 class="font-serif text-lg text-gray-800 font-medium group-hover:text-[#C5A059] transition-colors">
									{item.name}
								</h3>
								<span class="font-serif text-lg font-bold text-[#C5A059]">{item.price}</span>
							</div>
							<p class="text-gray-500 text-sm font-light leading-relaxed">{item.desc}</p>
							{#if item.dietary}
								<span class="text-[10px] text-gray-400 uppercase tracking-wider mt-1 block">{item.dietary === 'V' ? 'Vegetarian' : item.dietary}</span>
							{/if}
						</div>
					</div>
				{/each}
			</div>
		</div>

		<!-- --- FEATURE IMAGE BREAK --- -->
		<div class="w-full h-[400px] mb-24 relative rounded-sm overflow-hidden">
			<img 
				src="https://images.unsplash.com/photo-1594041680534-e8c8cdebd659?auto=format&fit=crop&q=80&w=1600" 
				alt="Platter"
				class="w-full h-full object-cover"
			/>
			<div class="absolute bottom-0 left-0 bg-white p-8 max-w-sm">
				<h4 class="font-serif text-2xl mb-2">The Istanbul Platter</h4>
				<p class="text-sm text-gray-500 mb-4">A curated selection of our finest charcoal grills, perfect for sharing.</p>
				<span class="text-[#C5A059] text-xs font-bold uppercase tracking-widest cursor-pointer hover:text-black">View Details</span>
			</div>
		</div>

		<!-- --- GRILLS SECTION --- -->
		<div id="grills" class="mb-24 scroll-mt-32">
			<div class="text-center mb-12">
				<div class="w-16 h-[1px] bg-[#C5A059] mx-auto mb-6"></div>
				<h2 class="font-serif text-4xl text-gray-900 uppercase tracking-wide">Charcoal Grills</h2>
				<p class="text-gray-500 text-sm italic mt-2">Cooked over traditional oak charcoal</p>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-2 gap-x-16 gap-y-10">
				{#each menuItems.grills as item}
					<div class="group flex gap-4 items-start">
						{#if item.image}
							<button 
								type="button"
								onclick={() => selectedImages = item.images || [item.image]} 
								class="shrink-0 bg-transparent border-none p-0 cursor-pointer" 
								aria-label="View full image"
							>
								<img src={item.image} alt={item.name} class="w-20 h-20 object-cover rounded-sm shadow-md hover:opacity-80 transition-opacity" />
							</button>
						{/if}
						<div class="flex-1">
							<div class="flex justify-between items-baseline mb-2 border-b border-dotted border-gray-300 pb-1">
								<h3 class="font-serif text-lg text-gray-800 font-medium group-hover:text-[#C5A059] transition-colors">
									{item.name}
								</h3>
								<span class="font-serif text-lg font-bold text-[#C5A059]">{item.price}</span>
							</div>
							<p class="text-gray-500 text-sm font-light leading-relaxed">{item.desc}</p>
						</div>
					</div>
				{/each}
			</div>
		</div>

		<!-- --- STEAKS SECTION (Darker Theme Block) --- -->
		<div id="steaks" class="bg-[#1a1a1a] text-white p-10 md:p-16 -mx-6 md:-mx-20 mb-24 relative overflow-hidden scroll-mt-32 rounded-lg shadow-2xl">
			<!-- Background Texture Effect -->
			<div class="absolute top-0 right-0 w-64 h-64 bg-[#C5A059] rounded-full filter blur-[100px] opacity-10"></div>
			
			<div class="relative z-10">
				<div class="text-center mb-12">
					<span class="text-[#C5A059] tracking-[0.2em] text-xs font-bold uppercase mb-2 block">Premium Cuts</span>
					<h2 class="font-serif text-4xl uppercase tracking-wide text-white">Signature Steaks</h2>
				</div>

				<div class="grid grid-cols-1 md:grid-cols-2 gap-x-16 gap-y-12">
					{#each menuItems.steaks as item}
						<div class="group flex gap-4 items-start">
							{#if item.image}
								<button 
									type="button"
									onclick={() => selectedImages = item.images || [item.image]} 
									class="shrink-0 bg-transparent border-none p-0 cursor-pointer" 
									aria-label="View full image"
								>
									<img src={item.image} alt={item.name} class="w-20 h-20 object-cover rounded-sm shadow-lg border border-gray-700 hover:opacity-80 transition-opacity" />
								</button>
							{/if}
							<div class="flex-1">
								<div class="flex justify-between items-baseline mb-2 border-b border-gray-700 pb-2">
									<h3 class="font-serif text-xl font-medium text-[#C5A059] group-hover:text-white transition-colors">
										{item.name}
									</h3>
									<span class="font-serif text-xl font-light">{item.price}</span>
								</div>
								<p class="text-gray-400 text-sm font-light leading-relaxed">{item.desc}</p>
							</div>
						</div>
					{/each}
				</div>
			</div>
		</div>

		<!-- --- DESSERTS SECTION --- -->
		<div id="desserts" class="scroll-mt-32">
			<div class="text-center mb-12">
				<h2 class="font-serif text-4xl text-gray-900 uppercase tracking-wide">Desserts</h2>
				<div class="w-12 h-1 bg-[#C5A059] mx-auto mt-4"></div>
			</div>

			<div class="flex flex-col md:flex-row gap-12 items-center">
				<div class="md:w-1/2 w-full">
					<enhanced:img 
						src={baklava} 
						alt="Baklava" 
						class="w-full h-80 object-cover shadow-lg"
					/>
				</div>
				<div class="md:w-1/2 w-full space-y-10">
					{#each menuItems.desserts as item}
						<div class="group flex gap-4 items-start">
							{#if item.image}
								<button 
									type="button"
									onclick={() => selectedImages = item.images || [item.image]} 
									class="shrink-0 bg-transparent border-none p-0 cursor-pointer" 
									aria-label="View full image"
								>
									<img src={item.image} alt={item.name} class="w-16 h-16 object-cover rounded-sm shadow-md hover:opacity-80 transition-opacity" />
								</button>
							{/if}
							<div class="flex-1">
								<div class="flex justify-between items-baseline mb-2">
									<h3 class="font-serif text-lg text-gray-800 font-medium">{item.name}</h3>
									<span class="font-serif text-lg text-[#C5A059]">{item.price}</span>
								</div>
								<p class="text-gray-500 text-sm font-light">{item.desc}</p>
							</div>
						</div>
					{/each}
				</div>
			</div>
		</div>

	</div>

	<!-- --- FOOTER (Same as Layout) --- -->
	<footer class="bg-[#0a0a0a] text-white pt-20 pb-8 border-t-[3px] border-[#C5A059]">
		<div class="container mx-auto px-6">
			<div class="flex flex-col md:flex-row justify-between items-start mb-16 gap-10">
				<div class="max-w-sm">
					<div class="font-serif text-2xl tracking-widest mb-6">ISTANBUL</div>
					<h5 class="text-xs font-bold text-gray-400 uppercase tracking-widest mb-4">Join our list</h5>
					<div class="flex border-b border-gray-700 pb-2">
						<input type="email" placeholder="Enter your email address" class="bg-transparent border-none outline-none text-white w-full placeholder-gray-600 text-sm" />
						<button class="text-xs font-bold uppercase text-[#C5A059] tracking-widest">Subscribe</button>
					</div>
				</div>
				<div class="grid grid-cols-2 md:grid-cols-3 gap-x-12 gap-y-8 text-xs text-gray-400 font-light leading-loose">
					<div>
						<h6 class="text-white font-bold uppercase tracking-wider mb-4 text-[10px]">Restaurant</h6>
						<ul class="space-y-1">
							<li class="hover:text-[#C5A059] cursor-pointer">About Us</li>
							<li class="hover:text-[#C5A059] cursor-pointer">Private Dining</li>
							<li class="hover:text-[#C5A059] cursor-pointer">Gift Vouchers</li>
						</ul>
					</div>
					<div>
						<h6 class="text-white font-bold uppercase tracking-wider mb-4 text-[10px]">Contact</h6>
						<ul class="space-y-1">
							<li class="hover:text-[#C5A059] cursor-pointer">+258 84 123 4567</li>
							<li class="hover:text-[#C5A059] cursor-pointer">info@istanbul.co.mz</li>
							<li class="hover:text-[#C5A059] cursor-pointer">Maputo, Mozambique</li>
						</ul>
					</div>
					<div>
						<h6 class="text-white font-bold uppercase tracking-wider mb-4 text-[10px]">Follow Us</h6>
						<div class="flex gap-4 mt-2">
							<Instagram size={18} class="hover:text-[#C5A059] cursor-pointer" />
							<Facebook size={18} class="hover:text-[#C5A059] cursor-pointer" />
						</div>
					</div>
				</div>
			</div>
			<div class="border-t border-gray-900 pt-8 flex flex-col md:flex-row justify-between items-center gap-6">
				<div class="text-[10px] text-gray-600 uppercase tracking-widest text-center">
					© 2024 Istanbul Restaurant. All Rights Reserved.
				</div>
			</div>
		</div>
	</footer>
</div>

<!-- --- IMAGE MODAL (Moved outside main div) --- -->
{#if selectedImages}
	<ImageViewer images={selectedImages} onClose={() => selectedImages = null} />
{/if}

<style>
	.font-serif { font-family: 'Playfair Display', serif; }
	.font-sans { font-family: 'Lato', sans-serif; }
	
	.scrollbar-hide::-webkit-scrollbar {
		display: none;
	}
	.scrollbar-hide {
		-ms-overflow-style: none;
		scrollbar-width: none;
	}

	@keyframes fadeInUp {
		from {
			opacity: 0;
			transform: translate3d(0, 40px, 0);
		}
		to {
			opacity: 1;
			transform: translate3d(0, 0, 0);
		}
	}

	.animate-fade-in-up {
		animation: fadeInUp 0.8s ease-out forwards;
	}
</style>
