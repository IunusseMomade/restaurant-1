<script>
  // Remove unused social/menu icons (footer is now shared)
  import { Award, Flame, Wine, ChefHat } from '@lucide/svelte';

  import person_1 from '$lib/assets/images/about/about-section4-1.jpeg?enhanced';
  import person_2 from '$lib/assets/images/about/about-section4-2.jpeg?enhanced';
  import ambient_1 from '$lib/assets/images/about/about-section2-1.jpeg?enhanced';
  import food_1 from '$lib/assets/images/about/about-section2-2.jpeg?enhanced';
  import about_header from '$lib/assets/images/about-header.jpeg?enhanced';

  import HeaderSimple from '$lib/components/HeaderSimple.svelte';
  import Footer from '$lib/components/Footer.svelte';

  import * as m from '$lib/paraglide/messages';
  import { page } from '$app/state';
  import { localizeHref } from '$lib/paraglide/runtime';

  const seoTitle = m.about_seo_title();
  const seoDescription = m.about_seo_description();
  const canonical = $derived(() => `${$page.url.origin}${$page.url.pathname}`.replace(/\/$/, ''));
</script>

<svelte:head>
  <title>{seoTitle}</title>
  <meta name="description" content={seoDescription} />
  <meta name="robots" content="index,follow,max-image-preview:large" />
  <link rel="canonical" href={canonical} />

  <meta property="og:type" content="website" />
  <meta property="og:title" content={seoTitle} />
  <meta property="og:description" content={seoDescription} />
  <meta property="og:url" content={canonical} />
  <meta property="og:site_name" content="Istanbul Restaurant" />
  <meta property="og:locale" content="pt_MZ" />

  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content={seoTitle} />
  <meta name="twitter:description" content={seoDescription} />
</svelte:head>

<div class="min-h-screen bg-white text-gray-800 font-sans selection:bg-[#C5A059] selection:text-white">
	<HeaderSimple />

	<!-- --- 2. HERO SECTION --- -->
	<section class="relative w-full h-[70vh] flex items-center justify-center overflow-hidden">
		<div class="absolute inset-0">
			<!-- <video
				autoplay
				muted
				loop
				playsinline
				poster="https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&q=80&w=2000"
				class="w-full h-full object-cover"
			>
				<source src="https://videos.pexels.com/video-files/3196236/3196236-uhd_2560_1440_25fps.mp4" type="video/mp4" />
				Your browser does not support the video tag.
			</video> -->
			<enhanced:img
			  alt="foto istanbul restaurant dentro"
			  src={about_header}
			  class="w-full h-full object-cover"
			/>
			<div class="absolute inset-0 bg-black/60"></div>
		</div>
		
		<div class="relative z-10 text-center text-white px-6 max-w-4xl mx-auto animate-fade-in-up">
			<div class="w-20 h-[1px] bg-[#C5A059] mx-auto mb-8"></div>
			<h1 class="font-serif text-5xl md:text-7xl mb-6 leading-tight tracking-tight">
				{m.about_hero_h1()}
			</h1>
			<p class="text-gray-200 font-light text-lg md:text-xl tracking-wide leading-relaxed">
				{m.about_hero_subtitle()}
			</p>
		</div>
	</section>

	<!-- --- 3. ABOUT / STORY --- -->
	<section class="py-20 md:py-32 container mx-auto px-6">
		<div class="grid grid-cols-1 lg:grid-cols-2 gap-16 lg:gap-24 items-center">
			<!-- Text Side -->
			<div class="order-2 lg:order-1">
				<span class="text-[#C5A059] text-xs font-bold uppercase tracking-[0.2em] mb-4 block">
					{m.about_section_label()}
				</span>

				<h2 class="font-serif text-4xl md:text-5xl text-gray-900 mb-8 leading-tight">
					{@html m.about_h2_html()}
				</h2>

				<div class="space-y-6 text-gray-500 font-light text-base leading-8">
					<p>{m.about_p1()}</p>
					<p>{m.about_p2()}</p>
					<p>
						{m.about_p3_prefix()}
						<em>{m.about_keyword_phrase()}</em>.
					</p>
				</div>

				<div class="mt-10">
					<enhanced:img src={person_2} alt={m.about_alt_ambience()} />
				</div>

				<div class="mt-8 flex flex-wrap gap-3">
					<a
						href={localizeHref('/menu')}
						class="bg-[#C5A059] text-white px-6 py-3 text-xs font-bold uppercase tracking-widest hover:bg-[#a68545] transition-colors shadow-sm"
					>
						{m.about_btn_menu()}
					</a>
					<a
						href={localizeHref('/contact')}
						class="border border-gray-300 text-gray-900 px-6 py-3 text-xs font-bold uppercase tracking-widest hover:border-[#C5A059] hover:text-[#C5A059] transition-colors"
					>
						{m.about_btn_contact()}
					</a>
				</div>
			</div>

			<!-- Image Side - Collage Effect -->
			<div class="order-1 lg:order-2 relative">
				<div class="relative z-10">
					<enhanced:img
						src={ambient_1}
						alt={m.about_alt_ambient_main()}
						class="w-full h-auto shadow-2xl"
					/>
				</div>

				<div class="absolute -bottom-12 -left-12 w-2/3 z-20 hidden md:block">
					<enhanced:img
						src={food_1}
						alt={m.about_alt_food_detail()}
						class="w-full h-auto shadow-xl border-8 border-white"
					/>
				</div>
			</div>
		</div>
	</section>

	<!-- --- 4. PILLARS OF EXCELLENCE (Icons) --- -->
	<section class="bg-[#FAFAFA] py-24 border-t border-gray-100">
		<div class="container mx-auto px-6">
			<div class="grid grid-cols-1 md:grid-cols-4 gap-12 text-center">
				
				<div class="flex flex-col items-center group">
					<div class="w-16 h-16 rounded-full bg-white border border-gray-200 flex items-center justify-center mb-6 shadow-sm group-hover:border-[#C5A059] transition-colors">
						<Flame class="text-gray-800 group-hover:text-[#C5A059] transition-colors" size={28} />
					</div>
					<h4 class="font-serif text-lg mb-3">{m.about_pillar1_title()}</h4>
					<p class="text-xs text-gray-500 uppercase tracking-widest leading-relaxed">
						{m.about_pillar1_desc()}
					</p>
				</div>

				<div class="flex flex-col items-center group">
					<div class="w-16 h-16 rounded-full bg-white border border-gray-200 flex items-center justify-center mb-6 shadow-sm group-hover:border-[#C5A059] transition-colors">
						<Award class="text-gray-800 group-hover:text-[#C5A059] transition-colors" size={28} />
					</div>
					<h4 class="font-serif text-lg mb-3">{m.about_pillar2_title()}</h4>
					<p class="text-xs text-gray-500 uppercase tracking-widest leading-relaxed">
						{m.about_pillar2_desc()}
					</p>
				</div>

				<div class="flex flex-col items-center group">
					<div class="w-16 h-16 rounded-full bg-white border border-gray-200 flex items-center justify-center mb-6 shadow-sm group-hover:border-[#C5A059] transition-colors">
						<Wine class="text-gray-800 group-hover:text-[#C5A059] transition-colors" size={28} />
					</div>
					<h4 class="font-serif text-lg mb-3">{m.about_pillar3_title()}</h4>
					<p class="text-xs text-gray-500 uppercase tracking-widest leading-relaxed">
						{m.about_pillar3_desc()}
					</p>
				</div>

				<div class="flex flex-col items-center group">
					<div class="w-16 h-16 rounded-full bg-white border border-gray-200 flex items-center justify-center mb-6 shadow-sm group-hover:border-[#C5A059] transition-colors">
						<ChefHat class="text-gray-800 group-hover:text-[#C5A059] transition-colors" size={28} />
					</div>
					<h4 class="font-serif text-lg mb-3">{m.about_pillar4_title()}</h4>
					<p class="text-xs text-gray-500 uppercase tracking-widest leading-relaxed">
						{m.about_pillar4_desc()}
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- --- 5. FEATURE SECTION (Dark) --- -->
	<section class="bg-[#111] text-white py-24 md:py-32 relative overflow-hidden">
		<!-- Background Texture -->
		<div class="absolute top-0 left-0 w-full h-full opacity-10 pointer-events-none">
		   <svg width="100%" height="100%">
			 <pattern id="pattern-circles" x="0" y="0" width="40" height="40" patternUnits="userSpaceOnUse">
			   <circle cx="2" cy="2" r="1" fill="#fff" />
			 </pattern>
			 <rect x="0" y="0" width="100%" height="100%" fill="url(#pattern-circles)" />
		   </svg>
		</div>

		<div class="container mx-auto px-6 relative z-10">
			<div class="flex flex-col md:flex-row items-center gap-16">
				<div class="md:w-1/2">
					<div class="relative">
						<enhanced:img src={person_1} alt={m.about_alt_experience()} class="w-full h-[500px] object-cover " />
					</div>
				</div>
				
				<div class="md:w-1/2">
					<Award class="text-[#C5A059] mb-6" size={40} />
					<h2 class="font-serif text-4xl md:text-5xl mb-8 leading-tight">
						{m.about_feature_title()}
					</h2>
					<div class="w-16 h-1 bg-[#C5A059] mb-8"></div>
					<p class="text-gray-400 font-light leading-relaxed mb-8">{m.about_feature_desc()}</p>

					<a
						href={localizeHref('/menu')}
						class="inline-block border border-white text-white px-8 py-3 text-xs font-bold uppercase tracking-widest hover:bg-[#C5A059] hover:border-[#C5A059] transition-all"
					>
						{m.about_feature_btn()}
					</a>
				</div>
			</div>
		</div>
	</section>

	<!-- --- 6. CTA --- -->
	<section class="py-24 text-center">
		<div class="container mx-auto px-6">
			<h2 class="font-serif text-4xl text-gray-900 mb-6">{m.about_cta_title()}</h2>
			<p class="text-gray-500 font-light max-w-2xl mx-auto mb-10">{m.about_cta_desc()}</p>
			<a
				href={localizeHref('/contact')}
				class="inline-block bg-[#C5A059] text-white px-10 py-4 text-sm font-bold uppercase tracking-[0.15em] hover:bg-[#a68545] transition-all shadow-xl hover:shadow-2xl transform hover:-translate-y-1"
			>
				{m.about_cta_btn()}
			</a>
		</div>
	</section>

	<Footer />
</div>

<style>
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

	@media (prefers-reduced-motion: reduce) {
		.animate-fade-in-up {
			animation: none;
		}
	}
</style>
